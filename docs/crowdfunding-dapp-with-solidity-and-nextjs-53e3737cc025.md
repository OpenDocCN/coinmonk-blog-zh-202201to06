# 用 Solidity 和 NextJS 众筹 dApp

> 原文：<https://medium.com/coinmonks/crowdfunding-dapp-with-solidity-and-nextjs-53e3737cc025?source=collection_archive---------11----------------------->

我是一个相当新的开发人员，我发现当我构建一个项目时学习编码是最容易的，所以我决定构建一个。

我建立了一个不需要中介的众筹网站。终端用户进来，开始与平台互动。你可以[在这里](https://crowd-fund-darkmatterchimpanzee.vercel.app/)查看。

好了，说够了，让我们开始吧。

我们从用我的主目录初始化 truffle 开始:

```
truffle init
```

我喜欢使用 ganache appimage，所以启动它，它会在端口 8545 上为我们生成一个本地测试网。

进入我的 truffle.config.js 进行必要的修改

```
const HDWalletProvider = require('[@truffle/hdwallet-provider](http://twitter.com/truffle/hdwallet-provider)');const fs = require('fs');const mnemonic = fs.readFileSync(".secret").toString().trim();require('dotenv').config();const projectID = process.env.PROJECT_ID;module.exports = {networks: {
   development: {
      host: "127.0.0.1",     // Localhost (default: none)
      port: 8545,            // Standard Ethereum port (default: none)
      network_id: "*",       // Any network (default: none)
   },
   rinkeby: {// 1.
      provider: () => new HDWalletProvider(mnemonic, `[https://rinkeby.infura.io/v3/${projectID}`](https://rinkeby.infura.io/v3/${projectID}`)),
      network_id: "4", // Rinkeby ID 4
      gas: 4465030,
      gasPrice: 10000000000,
   }
},// Set default mocha options here, use special reporters etc.mocha: {
// timeout: 100000
},// Configure your compilerscompilers: {
      solc: {
         version: "0.8.4",      // Fetch exact version from solc-bin (default: truffle's version)
      settings: {          
         optimizer: {
            enabled: true,
            runs: 200
         },
      }
   }
  },
};
```

我最终在 rinkeby testnet 上托管了这个项目，所以我在这里添加了 infura 端点。

转到 infura dashboard，注册并为您的项目设置一个端点。[说明在这里](https://blog.infura.io/post/introducing-the-infura-dashboard-8969b7ab94e7)。一旦你建立了一个项目，进入设置，复制项目的 ID 并粘贴到根目录下的. env 文件中

```
PROJECT_ID=db0b4735bad24926a761d909e1f82576
```

因为这个项目是公开的，所以我把它放在这里。你不会想在制作过程中这样做的。与危及安全有关。我不知道具体的原因，但钻研安全是我的下一步行动，所以有一天我会写一个帖子，我会知道为什么这是不安全的。

助记符是最终将它部署到 testnet 的帐户的私钥，所以确保在部署之前从 rinkeby 水龙头那里得到一些假的 ETH。

我将代码放在这里，因为它有很好的文档记录并且不言自明:

[github 回购在这里](https://github.com/darkMatterChimpanzee/crowdFund)。相信我，你想看那里的代码，而不是这个巨大的没有颜色的怪物。

我通常喜欢在一开始就定义合同中的所有事件，因为这让我对合同中将要发生的所有事情有所了解

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;import "[@openzeppelin/contracts](http://twitter.com/openzeppelin/contracts)/utils/math/SafeMath.sol";
import "[@openzeppelin/contracts](http://twitter.com/openzeppelin/contracts)/security/ReentrancyGuard.sol";contract CrowdFund is ReentrancyGuard {
    using SafeMath for uint256;/*===== Events =====*/
    event NewProjectCreated(
        uint256 indexed id,
        address projectCreator,
        string projectTitle,
        string projectDesc,
        uint256 projectDeadline,
        uint256 goalAmount
    );event ExpireFundraise(
        uint256 indexed id,
        string name,
        uint256 projectDeadline,
        uint256 goal
    );

    event SuccessFundRaise(
        uint256 indexed id,
        string name,
        uint256 projectDeadline,
        uint256 goal
    );

    event SuccessButContinueFundRaise(
        uint256 indexed id,
        string name,
        uint256 projectDeadline,
        uint256 goal
    );event FundsReceive(
        uint256 indexed id,
        address contributor,
        uint256 amount,
        uint256 totalPledged
    );event NewWithdrawalRequest(
        uint256 indexed id,
        string description,
        uint256 amount
    );event GenerateRefund(
        uint256 indexed id,
        address refundRequestUser,
        uint256 refundAmt
    );event ApproveRequest(uint256 indexed _id, uint32 _withdrawalRequestIndex);event RejectRequest(uint256 indexed _id, uint32 _withdrawalRequestIndex);event TransferRequestFunds(
        uint256 indexed _id,
        uint32 _withdrawalRequestIndex
    );event PayCreator( uint256 indexed _id, uint32 _withdrawalRequestIndex, uint256 _amountTransfered);event PayPlatform(uint256 indexed _id, uint32 _withdrawalRequestIndex, uint256 _amountTransfered);
```

接下来，我们定义所有的状态变量。这些都是有状态的东西，在与用户互动的过程中会有某种转变。

```
/*===== State variables =====*/
    address payable platformAdmin;enum State {
        Fundraise,
        Expire,
        Success
    }enum Withdrawal {
        Allow,
        Reject
    }struct Project {
        // project ID
        uint256 id;
        // address of the creator of project
        address payable creator;
        // name of the project
        string name;
        // description of the project
        string description;
        // end of fundraising date
        uint256 projectDeadline;
        // total amount that has been pledged until this point
        uint256 totalPledged;
        // total amount needed for a successful campaign
        uint256 goal;
        // number of depositors
        uint256 totalDepositors;
        // total funds withdrawn from project
        uint256 totalWithdrawn;
        // current state of the fundraise
        State currentState;
        // holds URL of IPFS upload
        // string ipfsURL;
    }struct WithdrawalRequest {
        uint32 index;
        // purpose of withdrawal
        string description;
        // amount of withdrawal requested
        uint256 withdrawalAmount;
        // project owner address
        address payable recipient;
        // total votes received for request
        uint256 approvedVotes;
        // current state of the withdrawal request
        Withdrawal currentWithdrawalState;
        // hash of the ipfs storage
        // string ipfsHash;
        // boolean to represent if amount has been withdrawn
        bool withdrawn;
    }mapping(address => uint) balances;// project states
    uint256 public projectCount;
    mapping(uint256 => Project) public idToProject;
    // project id => contributor => contribution
    mapping(uint256 => mapping(address => uint256)) public contributions;// withdrawal requests
    mapping(uint256 => WithdrawalRequest[]) public idToWithdrawalRequests;
    // project ID => withdrawal request Index
    mapping(uint256 => uint32) latestWithdrawalIndex;// project id => request number => address of contributors
    mapping(uint256 => mapping(uint32 => address[])) approvals;
    mapping(uint256 => mapping(uint32 => address[])) rejections;
```

接下来，我们放入一些修饰符来严格限制谁可以与契约函数交互。

```
/*===== Modifiers =====*/
    modifier checkState(uint256 _id, State _state) {
        require(
            idToProject[_id].currentState == _state,
            "Unmatching states. Invalid operation"
        );
        _;
    }modifier onlyAdmin() {
        require(
            msg.sender == platformAdmin,
            "Unauthorized access. Only admin can use this function"
        );
        _;
    }modifier onlyProjectOwner(uint256 _id) {
        require(
            msg.sender == idToProject[_id].creator,
            "Unauthorized access. Only project owner can use this function"
        );
        _;
    }modifier onlyProjectDonor(uint256 _id) {
        require(
            contributions[_id][msg.sender] > 0,
            "Unauthorized access. Only project funders can use this function."
        );
        _;
    }modifier checkLatestWithdrawalIndex(
        uint256 _id,
        uint32 _withdrawalRequestIndex
    ) {
        require(
            latestWithdrawalIndex[_id] == _withdrawalRequestIndex,
            "This is not the latest withdrawal request. Please check again and try later"
        );
        _;
    }
```

我加了一个重入守卫，因为我只是不想让人们在这种公共利益上做贪婪的事情。

这个契约的后备是平台管理员。如果有一些乙醚漂浮在周围，还不如把它发送给管理员，而不是浪费在合同上。

```
constructor() ReentrancyGuard() {
        platformAdmin = payable(msg.sender);
        projectCount = 0;
    }// make contract payable
    fallback() external payable {}
    receive() external payable {
        platformAdmin.transfer(msg.value);
    }/*===== Functions  =====*//** [@dev](http://twitter.com/dev) Function to start a new project.
     * [@param](http://twitter.com/param) _name Name of the project
     * [@param](http://twitter.com/param) _description Project Description
     * [@param](http://twitter.com/param) _projectDeadline Total days to end of fundraise
     * [@param](http://twitter.com/param) _goalEth Project goal in ETH
     */
    function createNewProject(
        string memory _name,
        string memory _description,
        uint256 _projectDeadline,
        uint256 _goalEth
    ) public {
        // update ID
        projectCount += 1; // log goal as wei
        uint256 _goal = _goalEth * 1e18; // create new fundraise object
        Project memory newFR = Project({
            id: projectCount,
            creator: payable(msg.sender),
            name: _name,
            description: _description,
            projectDeadline: _projectDeadline,
            totalPledged: 0,
            goal: _goal,
            currentState: State.Fundraise,
            totalDepositors: 0,
            totalWithdrawn: 0
        }); // update mapping of id to new project
        idToProject[projectCount] = newFR; // initiate total withdrawal requests 
        latestWithdrawalIndex[projectCount] = 0; // emit event
        emit NewProjectCreated(
            projectCount,
            msg.sender,
            _name,
            _description,
            _projectDeadline,
            _goal
        );
    }/** [@dev](http://twitter.com/dev) Function to make a contribution to the project
     * [@param](http://twitter.com/param) _id Project ID where contributions are to be made
     */
    function contributeFunds(uint256 _id)
        public
        payable
        checkState(_id, State.Fundraise)
        nonReentrant()
    {
        require(_id <= projectCount, "Project ID out of range"); require(
            msg.value > 0,
            "Invalid transaction. Please send valid amounts to the project"
        ); require(
            block.timestamp <= idToProject[_id].projectDeadline,
            "Contributions cannot be made to this project anymore."
        ); // transfer contributions to contract address
        balances[address(this)] += msg.value; // add to contribution
        contributions[_id][msg.sender] += msg.value; // increase total contributions pledged to the project
        idToProject[_id].totalPledged += msg.value; // add one to total number of depositors for this project
        idToProject[_id].totalDepositors += 1; emit FundsReceive(
            _id,
            msg.sender,
            msg.value,
            idToProject[_id].totalPledged
        );
    }/** [@dev](http://twitter.com/dev) Function to end fundraising drive
    * [@param](http://twitter.com/param) _id Project ID
    */
    function endContributionsExpire(uint256 _id) 
        public 
        onlyProjectDonor(_id)
        checkState(_id, State.Fundraise) 
        {
            require(
                block.timestamp > idToProject[_id].projectDeadline,
                "Invalid request. Can only be called after project deadline is reached"
            ); idToProject[_id].currentState = State.Expire;
            emit ExpireFundraise(_id,
                idToProject[_id].name,
                idToProject[_id].projectDeadline,
                idToProject[_id].goal
            );
        }

    /** [@dev](http://twitter.com/dev) Function to end fundraising drive with success is total pledged higher than goal. Irrespective of deadline
    * [@param](http://twitter.com/param) _id Project ID
    */
    function endContributionsSuccess(uint256 _id) 
        public 
        onlyProjectOwner(_id)
        checkState(_id, State.Fundraise) 
        {
            require(idToProject[_id].totalPledged >= idToProject[_id].goal, "Did not receive enough funds"); idToProject[_id].currentState = State.Success;
            emit SuccessFundRaise(
                _id,
                idToProject[_id].name,
                idToProject[_id].projectDeadline,
                idToProject[_id].goal
            );                
        }/** [@dev](http://twitter.com/dev) Function to get refund on expired projects
     * [@param](http://twitter.com/param) _id Project ID
     */
    function getRefund(uint256 _id)
        public
        payable
        onlyProjectDonor(_id)
        checkState(_id, State.Expire)
        nonReentrant()
    {
        require(
            block.timestamp > idToProject[_id].projectDeadline,
            "Project deadline hasn't been reached yet"
        ); address payable _contributor = payable(msg.sender);
        uint256 _amount = contributions[_id][msg.sender];
        (bool success, ) = _contributor.call{value: _amount}("");
        require(success, "Transaction failed. Please try again later.");
        emit GenerateRefund(_id, _contributor, _amount); // update project state
        idToProject[_id].totalPledged -= _amount;
        idToProject[_id].totalDepositors -= 1;
    }/** [@dev](http://twitter.com/dev) Function to create a request for withdrawal of funds
    * [@param](http://twitter.com/param) _id Project ID
    * [@param](http://twitter.com/param) _requestNumber Index of the request
    * [@param](http://twitter.com/param) _description  Purpose of withdrawal
    * [@param](http://twitter.com/param) _amount Amount of withdrawal requested in ETH
    */
    function createWithdrawalRequest(
        uint256 _id,
        uint32 _requestNumber,
        string memory _description,
        uint256 _amount
    ) public onlyProjectOwner(_id) checkState(_id, State.Success){
        require(idToProject[_id].totalWithdrawn < idToProject[_id].totalPledged, "Insufficient funds"); require(_requestNumber == latestWithdrawalIndex[_id] + 1, "Incorrect request number"); // convert ETH to Wei units
        uint256 _withdraw = _amount * 1e18; // create new withdrawal request
        WithdrawalRequest memory newWR = WithdrawalRequest({
            index: _requestNumber,
            description: _description,
            withdrawalAmount: _withdraw,
            // funds withdrawn to project owner
            recipient: idToProject[_id].creator,
            // initialized with no votes for request
            approvedVotes: 0,
            // state changes on quorum
            currentWithdrawalState: Withdrawal.Reject,
            withdrawn: false
        }); // update project to request mapping
        idToWithdrawalRequests[_id].push(newWR);

        latestWithdrawalIndex[_id] += 1; // emit event
        emit NewWithdrawalRequest(_id, _description, _amount);
    }/** [@dev](http://twitter.com/dev) Function to check whether a given address has approved a specific request
    * [@param](http://twitter.com/param) _id Project ID
    * [@param](http://twitter.com/param) _withdrawalRequestIndex Index of the withdrawal request
    * [@param](http://twitter.com/param) _checkAddress Address of the request initiator
    */
    function _checkAddressInApprovalsIterator(
        uint256 _id,
        uint32 _withdrawalRequestIndex, 
        address _checkAddress
    )
        internal
        view 
        returns(bool approved) 
    {
        // iterate over the array specific to this id and withdrawal request
        for (uint256 i = 0; i < approvals[_id][_withdrawalRequestIndex - 1].length; i++) {
            // if address is in the array, return true
            if(approvals[_id][_withdrawalRequestIndex - 1][i] == _checkAddress) {
                approved = true;
            }
        }
    }/** [@dev](http://twitter.com/dev) Function to check whether a given address has rejected a specific request
    * [@param](http://twitter.com/param) _id Project ID
    * [@param](http://twitter.com/param) _withdrawalRequestIndex Index of the withdrawal request
    * [@param](http://twitter.com/param) _checkAddress Address of the request initiator
    */
    function _checkAddressInRejectionIterator(
        uint256 _id,
        uint32 _withdrawalRequestIndex, 
        address _checkAddress
    ) 
        internal
        view
        returns(bool rejected) 
    {
        // iterate over the array specific to this id and withdrawal request
        for (uint256 i = 0; i < rejections[_id][_withdrawalRequestIndex - 1].length; i++) {
            // if address is in the array, return true
            if(rejections[_id][_withdrawalRequestIndex - 1][i] == _checkAddress) {
                rejected = true;
            }
        }
    }/** [@dev](http://twitter.com/dev) Function to approve withdrawal of funds
    * [@param](http://twitter.com/param) _id Project ID
    * [@param](http://twitter.com/param) _withdrawalRequestIndex Index of withdrawal request
    */
    function approveWithdrawalRequest(
        uint256 _id,
        uint32 _withdrawalRequestIndex
    )
        public
        onlyProjectDonor(_id)
        checkState(_id, State.Success)
        checkLatestWithdrawalIndex(_id, _withdrawalRequestIndex)
    {
        // confirm msg.sender hasn't approved request yet
        require(!_checkAddressInApprovalsIterator(_id, _withdrawalRequestIndex, msg.sender), 
                "Invalid operation. You have already approved this request"); require(!_checkAddressInRejectionIterator(_id, _withdrawalRequestIndex, msg.sender), 
                "Invalid operation. You have rejected this request"); // get total withdrawal requests made
        uint256 _lastWithdrawal = latestWithdrawalIndex[_id]; // iterate over all requests for this project
        for (uint256 i = 0; i < _lastWithdrawal; i++) {
            // if request number is equal to index
            if(i + 1 == _withdrawalRequestIndex) {
                // increment approval count
                idToWithdrawalRequests[_id][i].approvedVotes += 1;
            }
        } // push msg.sender to approvals list for this request
        approvals[_id][_withdrawalRequestIndex - 1].push(msg.sender);

        emit ApproveRequest(_id, _withdrawalRequestIndex);
    }/** [@dev](http://twitter.com/dev) Function to reject withdrawal of funds
     * [@param](http://twitter.com/param) _id Project ID
     * [@param](http://twitter.com/param) _withdrawalRequestIndex Index of withdrawal request
     */
    function rejectWithdrawalRequest(
        uint256 _id,
        uint32 _withdrawalRequestIndex
    )
        public
        onlyProjectDonor(_id)
        checkState(_id, State.Success)
        checkLatestWithdrawalIndex(_id, _withdrawalRequestIndex)
    {
        // confirm user hasn't approved request
        require(!_checkAddressInApprovalsIterator(_id, _withdrawalRequestIndex, msg.sender), 
                "Invalid operation. You have approved this request");
        require(!_checkAddressInRejectionIterator(_id, _withdrawalRequestIndex, msg.sender), 
                "Invalid operation. You have already rejected this request"); // get total withdrawal requests made
        uint256 _lastWithdrawal = latestWithdrawalIndex[_id]; // iterate over all requests for this project
        for (uint256 i = 0; i < _lastWithdrawal; i++) {
            // if request number is equal to index
            if(i + 1 == _withdrawalRequestIndex) {
                // if there hve been approvals, decrement
                if(idToWithdrawalRequests[_id][i].approvedVotes != 0) {
                    // decrement approval count
                    idToWithdrawalRequests[_id][i].approvedVotes -= 1;
                } 
                    // else if no one has approved request yet, keep approvals to 0
                else {
                    idToWithdrawalRequests[_id][i].approvedVotes == 0;
                }
            }
        } // add msg.sender to rejections list for this request
        rejections[_id][_withdrawalRequestIndex - 1].push(msg.sender);emit RejectRequest(_id, _withdrawalRequestIndex);
    }/** [@dev](http://twitter.com/dev) Function to transfer funds to project creator
     * [@param](http://twitter.com/param) _id Project ID
     * [@param](http://twitter.com/param) _withdrawalRequestIndex Index of withdrawal request
     */
    function transferWithdrawalRequestFunds(
        uint256 _id,
        uint32 _withdrawalRequestIndex
    )
        public
        payable
        onlyProjectOwner(_id)
        checkLatestWithdrawalIndex(_id, _withdrawalRequestIndex)
        nonReentrant()
    {
        require(
     // _withdrawalRequestIndex - 1 to accomodate 0 start of arrays
            idToWithdrawalRequests[_id][_withdrawalRequestIndex - 1].approvedVotes > (idToProject[_id].totalDepositors).div(2),
            "More than half the total depositors need to approve withdrawal request"
        ); require(idToWithdrawalRequests[_id][_withdrawalRequestIndex - 1].withdrawn == false, "Withdrawal has laready been made for this request"); require(idToWithdrawalRequests[_id][_withdrawalRequestIndex - 1].withdrawalAmount < idToProject[_id].totalPledged, "Insufficient funds"); WithdrawalRequest storage cRequest = idToWithdrawalRequests[_id][_withdrawalRequestIndex - 1]; // flat 0.3% platform fee
        uint256 platformFee = (cRequest.withdrawalAmount.mul(3)).div(1000);
        (bool pfSuccess, ) = payable(platformAdmin).call{value: platformFee}("");
        require(pfSuccess, "Transaction failed. Please try again later.");
        emit PayPlatform(_id, _withdrawalRequestIndex, platformFee);

        // transfer funds to creator
        address payable _creator = idToProject[_id].creator;
        uint256 _amount = cRequest.withdrawalAmount - platformFee;
        (bool success, ) = _creator.call{value: _amount}("");
        require(success, "Transaction failed. Please try again later.");
        emit PayCreator(_id, _withdrawalRequestIndex, _amount); // update states
        cRequest.withdrawn = true;
        idToProject[_id].totalWithdrawn += cRequest.withdrawalAmount; emit TransferRequestFunds(_id, _withdrawalRequestIndex);
    }
```

这将是基本功能。接下来是视图函数，允许前端查询区块链和显示状态。

```
/*===== Blockchain get functions =====*//** [@dev](http://twitter.com/dev) Function to get project details
     * [@param](http://twitter.com/param) _id Project ID
     */
    function getProjectDetails(uint256 _id)
        public
        view
        returns (
            address creator,
            string memory name,
            string memory description,
            uint256 projectDeadline,
            uint256 totalPledged,
            uint256 goal,
            uint256 totalDepositors,
            uint256 totalWithdrawn,
            State currentState)
    {
        creator = idToProject[_id].creator;
        name = idToProject[_id].name;
        description = idToProject[_id].description;
        projectDeadline = idToProject[_id].projectDeadline;
        totalPledged = idToProject[_id].totalPledged;
        goal = idToProject[_id].goal;
        totalDepositors = idToProject[_id].totalDepositors;
        totalWithdrawn = idToProject[_id].totalWithdrawn;
        currentState = idToProject[_id].currentState;
    }function getAllProjects() public view returns (Project[] memory) {
        uint256 _projectCount = projectCount; Project[] memory projects = new Project[](_projectCount);
        for (uint256 i = 0; i < _projectCount; i++) {
            uint256 currentId = i + 1;
            Project storage currentItem = idToProject[currentId];
            projects[i] = currentItem;
        }
        return projects;
    }function getProjectCount() public view returns (uint256 count) {
        count = projectCount;
    }function getAllWithdrawalRequests(uint256 _id)
        public
        view
        returns (WithdrawalRequest[] memory)
    {
        uint256 _lastWithdrawal = latestWithdrawalIndex[_id]; WithdrawalRequest[] memory withdrawals = new WithdrawalRequest[](
            _lastWithdrawal
        );
        for (uint256 i = 0; i < _lastWithdrawal; i++) {
            WithdrawalRequest storage currentRequest = idToWithdrawalRequests[_id][i];
            withdrawals[i] = currentRequest;
        } return withdrawals;
    }function getContributions(uint256 _id, address _contributor) public view returns(uint256) {
        return contributions[_id][_contributor];
    }
}
```

一旦写好了契约，就用

```
truffle migrate
```

在交易收据中，复制合同地址并创建一个名为 config.js 的文件

```
export const contractAddress = "0x53692f4BB9E072d481D42Ce2c9d919E2945aDac6";
```

这个地址是我最终将它部署到 rinkeby testenet 的地方。

是的，那有很多代码。

去散散步。亲吻你的伴侣。如果你没有伴侣，去和你感兴趣的人谈谈，当这种交流带来的失望开始出现时…从前端开始。

按照这里给出的指令通过[用 NextJS 初始化 Tailwind。](https://tailwindcss.com/docs/guides/nextjs)

不要草率，不要错过任何一步。正确的配置对于整个构建最终的工作非常重要。

所以我使用 localhost 设置，然后注释掉它们以激活 testnet 的半真实世界设置。但是当你在你的开发环境中工作的时候，把过程反过来，做更多的探索。

我开始喜欢 NextJS 了，因为它让我远离了所有不必要的工作，我可以专注于产品的开发。

在开始之前，让我们的 package.json 文件看起来一样

```
{
  "name": "crowdfund",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  },
  "resolutions": {
    "async": "^2.6.4",
    "node-fetch": "^2.6.7",
    "lodash": "^4.17.21",
    "underscore": "^1.12.1",
    "yargs-parser": "^5.0.1"
  },
  "dependencies": {
    "[@openzeppelin/contracts](http://twitter.com/openzeppelin/contracts)": "^4.6.0",
    "[@openzeppelin/test-helpers](http://twitter.com/openzeppelin/test-helpers)": "^0.5.15",
    "[@truffle/hdwallet-provider](http://twitter.com/truffle/hdwallet-provider)": "^2.0.8",
    "[@walletconnect/web3-provider](http://twitter.com/walletconnect/web3-provider)": "^1.7.8",
    "bignumber.js": "^9.0.2",
    "dotenv": "^16.0.1",
    "ipfs-http-client": "^56.0.3",
    "next": "12.1.6",
    "nextjs-progressbar": "^0.0.14",
    "react": "18.1.0",
    "react-dom": "18.1.0",
    "true-json-bigint": "^1.0.1",
    "web3": "^1.7.3",
    "web3modal": "^1.9.7"
  },
  "devDependencies": {
    "[@babel/plugin-syntax-top-level-a](http://twitter.com/babel/plugin-syntax-top-level-a)wait": "^7.14.5",
    "[@openzeppelin/truffle-upgrades](http://twitter.com/openzeppelin/truffle-upgrades)": "^1.15.0",
    "autoprefixer": "^10.4.7",
    "chai": "^4.3.6",
    "eslint": "8.16.0",
    "eslint-config-next": "12.1.6",
    "ethereum-waffle": "^3.0.0",
    "ethers": "^5.6.8",
    "postcss": "^8.4.14",
    "tailwindcss": "^3.0.24"
  }
}
```

现在快跑

```
yarn
```

这将安装该项目所需的所有依赖项。

接下来，进入 pages 目录和 _app.js 文件:

```
import { AccountContext } from '../context.js'
import { useState } from 'react'
import Link from 'next/link'
import Head from 'next/head'
import NextNProgress from "nextjs-progressbar";
import { ethers } from 'ethers'
import Web3Modal from 'web3modal'
import WalletConnectProvider from '[@walletconnect/web3-provider](http://twitter.com/walletconnect/web3-provider)'import '../styles/globals.css'function MyApp({ Component, pageProps }) {
  const [account, setAccount] = useState(null)// 1. async function getWeb3Modal() {
    const web3Modal = new Web3Modal({
      network: 'rinkeby',
      cacheProvider: false,
      providerOptions: {
        walletconnect: {
          package: WalletConnectProvider, // testnet deployement
          options: {
            infuraId: process.env.PROJECT_ID
          }, // localhost for dev
          // options: {
          //   rpc: { 1337: '[http://localhost:8545'](http://localhost:8545'), },
          //   chainId: 1337,
          // }
        },
      },
    })
    return web3Modal
  }//2. async function web3connect() {
    try {
      const web3Modal = await getWeb3Modal()
      const connection = await web3Modal.connect()
      const provider = new ethers.providers.Web3Provider(connection)
      const accounts = await provider.listAccounts()
      return accounts;
    } catch (err) {
      console.log('error:', err)
    }
  }// 3. // connect to wallet
  async function connect() {
    const accounts = await web3connect()
    setAccount(accounts)
  } return (
    <div className='min-h-screen w-screen font-mono'>
      <Head>
        <title>iFund</title>
        <meta name="description" content="Create New Fundraising Campaign" />
        <link rel="icon" href="/logo.png" />
      </Head>
      <div className='sm:h-10'>
        <nav className='flex mx-auto text-black-20/100'>
          <Link href="/">
            <a>
              <img src="/logo.png" alt="crowdFund logo" className='h-20 object-contain my-5 ml-5' />
            </a>
          </Link> <div className='flex'>// 4.
            {
              !account ?
                <div className='my-10 mx-10' >
                  <p>Pls connect to interact with this app</p>
                  <button className='rounded-md bg-pink-500 text-white p-3 ml-20' onClick={connect}>Connect</button>
                </div> :
                <p className='rounded-md my-10 bg-pink-500 text-white p-3 ml-20' >
                  {account[0].substr(0, 10) + "..."}
                </p>
            } {/* if you compile right now it will give an error as we haven't created this page yet. this is coming up next. */} <Link href="/create">
              <button className='rounded-md my-10 bg-pink-500 text-white p-3 ml-20' >Create New Fundraising Project</button>
            </Link>
          </div>
        </nav>
      </div>// 5\.     {/* drip account into the app */}
      <AccountContext.Provider value={account}>
        <NextNProgress />
        {account && <Component {...pageProps} connect={connect} />}
      </AccountContext.Provider>
    </div>)
}export default MyApp
```

1.  联系区块链
2.  从我们的元掩码 infura 端点调用区块链
3.  更新当前与区块链对话的帐户的状态

4.很简单。如果尚未连接任何帐户，请说“连接”。如果有东西连接上了，打印出账户的前几个字符

5.AccountContext 是我们添加的一个上下文，这样应用程序就可以随时了解连接到它的用户的任何变化

(你可以[在这里阅读更多关于上下文的信息](https://reactjs.org/docs/context.html#reactcreatecontext))

在 pages 目录之外，创建一个名为 context.js 的文件，并将它添加到

```
import { createContext } from 'react'export const AccountContext = createContext(null)
```

接下来，我们在名为 create.js 的页面目录中创建用于筹款的页面

```
import Link from "next/link"
import { useEffect, useState } from 'react' // new
import { useRouter } from 'next/router'
import Web3Modal from 'web3modal'
import { ethers } from 'ethers'// 1.import CrowdFund from "../build/contracts/CrowdFund.json"
import { contractAddress } from '../config'// 2.const initialState = { name: '', description: '', projectDeadline: '', goal: 0 };const Create = () => {
    // router to route back to home page
    const router = useRouter() const [project, setProject] = useState(initialState)
    const [contract, setContract] = useState(); // 3. useEffect(() => {
        // function to get contract address and update state
        async function getContract() {
            const web3Modal = new Web3Modal()
            const connection = await web3Modal.connect()
            const provider = new ethers.providers.Web3Provider(connection)
            const signer = provider.getSigner()
            let _contract = new ethers.Contract(contractAddress, CrowdFund.abi, signer)
            setContract(_contract);
        }
        getContract();
    }) // 4. async function saveProject() {
        // destructure project 
        const { name, description, projectDeadline, goal } = project
        try {
            // create project
            let transaction = await contract.createNewProject(name, description, projectDeadline, goal)// await successful transaction and reroute to home
            const x = await transaction.wait()
            if (x.status == 1) {
                router.push('/')
            }
        } catch (err) {
            window.alert(err)
        }
    }return (
        <div className="min-h-screen my-20 w-screen p-5">
            <main>
                <div className="rounded-md my-10 bg-pink-500 text-white p-3 w-20"><Link href="/"> Home </Link></div>
                <p className="text-center text-lg my-5">Create a new campaign!</p> // 5. <div className="bg-pink-500 text-black h-50 p-10 flex flex-col">
                    <input
                        onChange={e => setProject({ ...project, name: e.target.value })}
                        name='title'
                        placeholder='Give it a name ...'
                        className='p-2 my-2 rounded-md'
                        value={project.name}
                    />
                    <textarea
                        onChange={e => setProject({ ...project, description: e.target.value })}
                        name='description'
                        placeholder='Give it a description ...'
                        className='p-2 my-2 rounded-md'
                    />
                    <input
                        onChange={e => setProject({ ...project, projectDeadline: Math.floor(new Date() / 1000) + (e.target.value * 86400) })}
                        name='projectDeadline'
                        placeholder='Give it a deadline ... (in days)'
                        className='p-2 my-2 rounded-md'
                    />
                    <input
                        onChange={e => setProject({ ...project, goal: e.target.value })}
                        name='goalEth'
                        placeholder='Give it a goal ... (in ETH). Only integer values are valid'
                        className='p-2 my-2 rounded-md'
                    />
                    <button type='button' className="w-20 text-white rounded-md my-10 px-3 py-2 shadow-lg border-2" onClick={saveProject}>Submit</button>
                </div>
            </main>
        </div>
    )
}export default Create
```

1.  是为前端获取合同细节的地方。我们需要三样东西来讨论这个合同。它所在的区块链、合同的地址、合同的内容以及试图与之交互的用户。区块链和谁在和它说话，我们从 truffle migrate 给我们的构建中获取 in _app.js. contract 地址及其内容(ABI)。
2.  我将初始状态设置为我希望募捐到的条目的对象。这使得稍后通过输入更新状态变得容易。
3.  由于 NextJS 在服务器端将所有内容都转换成 HTML，如果我们在 useEffect 中不提及这段代码，我们会得到一个错误，因为当然只有在设置了提供者和签名者之后，才能联系契约。
4.  这只是调用了我们在契约中定义的 createNewProject 函数
5.  现在，我们获取用户输入并更新状态，然后将其发送到区块链，从而创建一个新项目

如果你跑了

```
yarn run dev
```

现在，这将编译，我们将有一个主页和一个创建项目页面。

现在我们可以创建项目了，我们需要查看创建者创建的所有项目。所以在主页(index.js)我们写道:

```
import {
    contractAddress
} from '../config'
import CrowdFund from "../build/contracts/CrowdFund.json"
import { ethers, BigNumber } from 'ethers'
import Link from 'next/link'// 1.const infuraKey = process.env.PROJECT_ID;export default function Home({ projects }) {
    return (
        <div className='min-h-screen my-20 w-screen p-5'>
            <p className='text-center font-bold'>test project --- Please connect to the Rinkeby testnet</p><div className='bg-pink-500 text-white p-10 rounded-md'>
                <div>
                    <p className='font-bold m-5'>How it Works</p>
                    <p className='my-3'>1\. Creator creates a new project </p><p className='my-3'>2\. Contributors contribute until deadline</p>
                    <p className='my-3'>3\. If total pledged doesn&apos;t get met on deadline date, contributors expire the project and refund donated funds back</p>
                    <p className='my-3'>4\. If total amount pledged reaches the goal, creator declares the fundraise a success</p>
                    <div className='my-3'>
                        <p className='my-3 ml-10'>a. creator makes a withdrawal request</p>
                        <p className='my-3 ml-10'>b. contributors vote on the request</p>
                        <p className='my-3 ml-10'>c. if approved, creator withdraws the amount requested to work on the project</p>
                    </div>
                </div>
            </div>
            <div className='text-black'>// 2.
                <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 pt-6">
                    {
                        projects.map((project, i) => (
                            <div key={i} className="border shadow rounded-xl overflow-hidden">
                                <div className="p-4">
                                    <p>ID: {BigNumber.from(project[0]).toNumber()}</p>
                                    <p className="my-6 text-2xl font-semibold">{project[2]}</p>
                                    <div>
                                        <p className="my-3 text-gray-400">{project[3]?.substr(0, 20) + "..."}</p>
                                        <p className="my-3"> Deadline:  {
                                            new Date((BigNumber.from(project[4]).toNumber()) * 1000).toLocaleDateString()
                                        } </p><p className="my-3"> Total Pledged:  {
                                            Math.round(ethers.utils.formatEther(project[5]))
                                        } ETH</p><p className="my-3"> Goal:  {
                                            ethers.utils.formatEther(project[6])
                                        } ETH </p>
                                    </div>// 3\. 
<Link href={`project/${BigNumber.from(project[0]).toNumber()}`} key={i}>
                                        <button className='rounded-md my-5 bg-pink-500 text-white p-3 mx-1'>Details</button>
                                    </Link>
                                </div>
                            </div>
                        ))
                    }
                </div>
            </div>
        </div >
    )
}// 4.export async function getServerSideProps() {
    let provider = new ethers.providers.JsonRpcProvider(`[https://rinkeby.infura.io/v3/${infuraKey}`](https://rinkeby.infura.io/v3/${infuraKey}`)) // localhost
    // let provider = new ethers.providers.JsonRpcProvider()const contract = new ethers.Contract(contractAddress, CrowdFund.abi, provider)
    const data = await contract.getAllProjects()
    return {
        props: {
            projects: JSON.parse(JSON.stringify(data))
        }
    }
}
```

1.  从获取 infura 密钥。环境文件
2.  我们从服务器端渲染得到的道具会被析构并作为项目出现。我们映射到这一点，可以孤立的个人项目，已经由用户在此合同上创建。

3.这是我们接下来创建的页面。该页面将暂时出错

4.是 NextJS 大放异彩的地方。它获取服务器端的所有项目，并对其进行预渲染。这使得整个渲染速度超快。

我向上帝发誓，我希望我能把这个代码块做得更宽一点，但是，唉，这就是格式。你必须与它抗争，或者在 github 上查看代码。

我非常喜欢动态路由，所以我们将使用它。在 pages 目录中，创建一个名为 project 的目录。在其中创建一个名为[id]的文件。射流研究…

这基本上允许我们做的是运行函数 getStaticPaths 和 getStaticProps，这实际上填充了我们已经决定要挂钩的所有可能的路径。在这个例子中，我们将项目 ID 与路线挂钩。

```
import { BigNumber, ethers, web3 } from 'ethers'
import Web3Modal from 'web3modal'
import { useState, useContext, useEffect } from 'react' // new
import { useRouter } from 'next/router'
import Link from 'next/link'import {
    contractAddress
} from '../../config'
import { AccountContext } from '../../context'
import CrowdFund from "../../build/contracts/CrowdFund.json"const infuraKey = process.env.PROJECT_ID;export default function Project({ project, projectID }) {
    useContext(AccountContext); const router = useRouter()
    const [contributionValue, setContributionValue] = useState(0); const [contract, setContract] = useState(); useEffect(() => {
        // function to get contract address and update state
        async function getContract() {
            const web3Modal = new Web3Modal()
            const connection = await web3Modal.connect()
            const provider = new ethers.providers.Web3Provider(connection)
            const signer = provider.getSigner()
            let _contract = new ethers.Contract(contractAddress, CrowdFund.abi, signer)
            setContract(_contract);
        }
        getContract();
    }) // Function to contribute funds to the project
    async function contribute() {
        try {
            // send contribution
            let transaction = await contract.contributeFunds(projectID, {
                value: ethers.utils.parseUnits(contributionValue, "ether")
            })
            // await transaction
            let x = await transaction.wait() // reroute to home page
            if (x.status == 1) {
                router.push('/')
            }
        } catch (err) {
            window.alert(err.message)
        }
    } // function to declare fundraise a success
    async function changeStateToSuccess() {
        try {
            let tx = await contract.endContributionsSuccess(projectID);
            let x = await tx.wait() if (x.status == 1) {
                router.push(`/project/${projectID}`);
                window.alert('Project state was successfully changed to : Success')
            }
        } catch (err) {
            window.alert(err.message)
        }
    } // function to declare fundraise a failure
    async function changeStateToExpire() {
        try {
            let tx = await contract.endContributionsExpire(projectID);
            let x = await tx.wait() if (x.status == 1) {
                window.alert('Project state was successfully changed to : Expire')
            }
        } catch (err) {
            window.alert(err.message)
        }
    }// function to process a refund on failed fundraise
    async function processRefund() {
        try {
            let tx = await contract.getRefund(projectID);
            let x = await tx.wait() if (x.status == 1) {
                window.alert('Successful Refund')
                router.push('/');
            }
        } catch (err) {
            window.alert(err.message)
        }
    }// 1. if (router.isFallback) {
        return <div>Loading...</div>
    }return (
        <div className='mt-20'>
            <div className='bg-pink-500 text-white p-20 rounded-md mx-5 mt-40'>
                <p className='my-6'><span className='font-bold'> Project Number: </span> {projectID}</p>
                <p className='my-6'><span className='font-bold'> Creator: </span> {project.creator}</p>
                <p className='my-6'><span className='font-bold'> Project Name: </span> {project.name}</p>
                <div className='break-words'>
                    <p className='my-6'><span className='font-bold'>Description:</span> {project.description}</p>
                </div>
                <p className='my-6'><span className='font-bold'>Crowdfund deadline:</span> {new Date((BigNumber.from(project.projectDeadline).toNumber()) * 1000).toLocaleDateString()}</p>
                <p className='my-6'><span className='font-bold'>Total ETH pledged:</span> {project.totalPledged} ETH</p>
                <p className='my-6'><span className='font-bold'>Fundraise Goal:</span> {project.goal} ETH</p>
                <p className='my-6'><span className='font-bold'>Total Contributors:</span> {project.totalDepositors}</p>
                <p className='my-6'><span className='font-bold'>Current State:</span> {project.currentState === 0 ? 'Fundraise Active' : (project.currentState === 1) ? 'Fundraise Expired' : 'Fundraise Success'}</p><p className='my-6'><span className='font-bold'>Total Withdrawals:</span> {project.totalWithdrawn} ETH</p><div className='text-center'>
                    <input
                        onChange={e => setContributionValue(e.target.value)}
                        type='number'
                        className='p-2 my-2 rounded-md text-black'
                        value={contributionValue}
                    />
                    <button onClick={contribute} className='rounded-md mt-20 my-10 bg-white text-pink-500 p-3 mx-4 shadow-md'>Contribute</button>
                </div><div className='grid sm:grid-col-1 md:grid-cols-2 sm:text-sm'>
                    <div className='grid grid-cols-1 px-10 sm:w-200 place-content-stretch'>
                        <button onClick={changeStateToSuccess} className='rounded-md mt-20 my-10 bg-white text-pink-500 p-3 shadow-lg flex-wrap'>Click here if fundraise was a success (project owner only)</button><Link href={`withdrawal/${projectID}`}>
                            <button className='rounded-md mt-20 my-10 bg-white text-pink-500 p-3 shadow-lg min-w-50'>Create Withdrawal Request</button>
                        </Link><Link href={`requests/${projectID}`}>
                            <button className='rounded-md mt-20 my-10 bg-white text-pink-500 p-3 shadow-lg flex-wrap'>Approve / Reject / Withdraw</button>
                        </Link>
                    </div><div className='grid grid-cols-1 px-10'>
                        <button onClick={changeStateToExpire} className='rounded-md mt-20 my-10 bg-white text-pink-500 p-3 shadow-lg w-50'>Click here if fundraise needs to be expired (contributors only)</button><button onClick={processRefund} className='rounded-md mt-20 my-10 bg-white text-pink-500 p-3 shadow-lg w-50'>Request Refund</button>
                    </div>
                </div>
            </div>
        </div >
    )
}// 2.export async function getStaticPaths() {
    let provider = new ethers.providers.JsonRpcProvider(`[https://rinkeby.infura.io/v3/${infuraKey}`](https://rinkeby.infura.io/v3/${infuraKey}`))// let provider = new ethers.providers.JsonRpcProvider()
    const contract = new ethers.Contract(contractAddress, CrowdFund.abi, provider)
    const data = await contract.getAllProjects()// populate the dynamic routes with the id
    const paths = data.map(d => ({ params: { id: BigNumber.from(d[0]).toString() } }))return {
        paths,
        fallback: true
    }
}// 3.// local fetch - change to ropsten/mainnet on deployement time
export async function getStaticProps({ params }) {
    // isolate ID from params
    const { id } = params // contact the blockchain
    let provider = new ethers.providers.JsonRpcProvider(`[https://rinkeby.infura.io/v3/${infuraKey}`](https://rinkeby.infura.io/v3/${infuraKey}`)) // localhost
    // let provider = new ethers.providers.JsonRpcProvider()
    const contract = new ethers.Contract(contractAddress, CrowdFund.abi, provider)
    const data = await contract.getProjectDetails(id); // parse received data into JSON
    let projectData = {
        creator: data.creator,
        name: data.name,
        description: data.description,
        projectDeadline: BigNumber.from(data.projectDeadline).toNumber(),
        totalPledged: ethers.utils.formatEther(data.totalPledged),
        goal: ethers.utils.formatEther(data.goal),
        totalDepositors: BigNumber.from(data.totalDepositors).toNumber(),
        totalWithdrawn: ethers.utils.formatEther(data.totalWithdrawn),
        currentState: data.currentState
    }// return JSON data belonging to this route
    return {
        props: {
            project: projectData,
            projectID: id
        },
    }
}
```

1.  当路由发生时，我们需要一个回退，否则页面就没有什么可呈现的，并且会出错
2.  获取项目 ID，并告诉 nextJS 路由将挂钩到什么。在我们的例子中，它是项目的 ID。
3.  接下来，我们传递在最后一次 getStaticPaths 调用中获得的参数来获取项目的数据。我们创建一个 JSON 对象，并将其作为 props 返回，该 props 被放入主函数的顶部输入。

如果项目成功，创建者需要提交退出请求。为此，我们在项目目录中创建了一个名为 retraction 的新文件夹。我们在其中创建了一个名为[id]的文件。js 和

```
import { BigNumber, ethers } from 'ethers'
import { useEffect, useState } from 'react'
import Web3Modal from 'web3modal'
import { useRouter } from 'next/router'import {
    contractAddress
} from '../../../config'
import CrowdFund from "../../../build/contracts/CrowdFund.json"const infuraKey = process.env.PROJECT_ID;const initialState = { requestNo: '', requestDescription: '', amount: 0 };export default function Withdrawal({ projectID }) {
    const router = useRouter() const [withdrawalRequest, setWithdrawalRequest] =    useState(initialState)
    const [contract, setContract] = useState(); useEffect(() => {
        // function to get contract address and update state
        async function getContract() {
            const web3Modal = new Web3Modal()
            const connection = await web3Modal.connect()
            const provider = new ethers.providers.Web3Provider(connection)
            const signer = provider.getSigner()
            let _contract = new ethers.Contract(contractAddress, CrowdFund.abi, signer)
            setContract(_contract);
        }
        getContract();
    }) async function requestWithdrawal() {
        const { requestNo, requestDescription, amount } = withdrawalRequest; try {
            let transaction = await contract.createWithdrawalRequest(projectID, requestNo, requestDescription, amount)
            const x = await transaction.wait() if (x.status == 1) {
                router.push(`/project/${projectID}`)
            }
        } catch (err) {
            window.alert(err.message)
        }
    } if (router.isFallback) {
        return <div>Loading...</div>
    } return (
        <div className='grid sm:grid-cols-1 lg:grid-cols-1 mt-20 '>
            <p className='text-center'>Only project creator can access this functionality on goal reached</p>
            <div className='bg-pink-500 text-black p-20 text-center rounded-md mx-5 flex flex-col'>
                <input
                    type='number'
                    onChange={e => setWithdrawalRequest({ ...withdrawalRequest, requestNo: e.target.value })}
                    name='requestNo'
                    placeholder='Request number...'
                    className='p-2 mt-5 rounded-md'
                    value={withdrawalRequest.requestNo} />
                <textarea
                    onChange={e => setWithdrawalRequest({ ...withdrawalRequest, requestDescription: e.target.value })}
                    name='requestDescription'
                    placeholder='Give it a description ...'
                    className='p-2 mt-5 rounded-md'
                />
                <input
                    onChange={e => setWithdrawalRequest({ ...withdrawalRequest, amount: e.target.value })}
                    name='amount'
                    placeholder='Withdrawal amount ... (in ETH). Only integer values are valid'
                    className='p-2 mt-5 rounded-md'
                />
                <button type='button' className="w-20 bg-white rounded-md my-10 px-3 py-2 shadow-lg border-2" onClick={requestWithdrawal}>Submit</button>
            </div>
        </div >
    )
}export async function getStaticPaths() {
    let provider = new ethers.providers.JsonRpcProvider(`[https://rinkeby.infura.io/v3/${infuraKey}`](https://rinkeby.infura.io/v3/${infuraKey}`))// localhost 
    // let provider = new ethers.providers.JsonRpcProvider()
    const contract = new ethers.Contract(contractAddress, CrowdFund.abi, provider)
    const data = await contract.getAllProjects()// populate the dynamic routes with the id
    const paths = data.map(d => ({ params: { id: BigNumber.from(d[0]).toString() } }))return {
        paths,
        fallback: true
    }
}// local fetch - change to ropsten/mainnet on deployement time
export async function getStaticProps({ params }) {
    // isolate ID from params
    const { id } = params// return JSON data belonging to this route
    return {
        props: {
            projectID: id
        },
    }
}
```

已经创建的提款请求需要分离出来，单独批准或拒绝，如果请求获得批准，创建者需要能够提取金额。

在项目目录中，创建一个名为 requests 的新目录。创建一个名为[id]的新文件。js 和

```
import { ethers, BigNumber } from 'ethers'
import Web3Modal from 'web3modal'
import { useEffect, useState } from 'react'
import { useRouter } from 'next/router'import {
    contractAddress
} from '../../../config'
import CrowdFund from "../../../build/contracts/CrowdFund.json"const infuraKey = process.env.PROJECT_ID;export default function Requests({ project, projectID }) {
    const router = useRouter()
    const [withdrawalRequests, setWithdrawalRequests] = useState([])
    const [contract, setContract] = useState(); useEffect(() => {
        // function to get contract address and update state
        async function getContract() {
            const web3Modal = new Web3Modal()
            const connection = await web3Modal.connect()
            const provider = new ethers.providers.Web3Provider(connection)
            const signer = provider.getSigner()
            let _contract = new ethers.Contract(contractAddress, CrowdFund.abi, signer)
            setContract(_contract);
        }
        getContract();
    }) // function to get all requests made by the creator async function getRequests() {
        try {
            let x = await contract.getAllWithdrawalRequests(projectID)
            setWithdrawalRequests(x);
        } catch (err) {
            window.alert(err.message)
        }
    } // function to approve a specific request async function approveRequest(r, projectID) {
        try {
            let tx = await contract.approveWithdrawalRequest(projectID, r[0])
            let x = await tx.wait()if (x.status == 1) {
                router.push(`/project/${projectID}`)
            }
        } catch (err) {
            window.alert(err.message)
        }
    } // function to reje a specific request async function rejectRequest(r, projectID) {
        try {
            let tx = await contract.rejectWithdrawalRequest(projectID, r[0])
            let x = await tx.wait()if (x.status == 1) {
                router.push(`/project/${projectID}`)
            }
        } catch (err) {
            window.alert(err.message)
        }
    }      // function to transfer funds to the creator if requests were approved
    async function transferFunds(r, projectID) {
        try {
            let tx = await contract.transferWithdrawalRequestFunds(projectID, r[0])
            let x = await tx.wait()if (x.status == 1) {
                router.push(`/project/${projectID}`)
            }
        } catch (err) {
            window.alert(err.message)
        }
    }
 if (router.isFallback) {
        return <div>Loading...</div>
    } return (
        <div className='grid sm:grid-cols-1 lg:grid-cols-1 mt-20 '>
            <p className='text-center'>Only project contributors can access approve/reject functionality</p>
            <p className='text-center mt-3 mb-3'>Creators need more than 50% of the contributors to approve a request before withdrawal can be made</p><div className='bg-pink-500 text-white p-20 text-center rounded-md'>
                <button onClick={getRequests} className="bg-white text-black rounded-md my-10 px-3 py-2 shadow-lg border-2 w-80">Get all withdrawal requests</button><p className='font-bold'>All Withdrawal requests</p><div className='grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 pt-6'>
                    {
                        withdrawalRequests.map(request =>
                            <div className='border shadow rounded-xl text-left grid grid-cols-1 lg:grid-col-2' key={request[0]}>
                                <div className='p-4'>
                                    <p className='py-4'>request number: {request[0]}</p>
                                    <p className='py-4 break-words'>description: {request[1]}</p>
                                    <p className='py-4'>amount: {ethers.utils.formatEther(request[2])} ETH</p>
                                    <p className='py-4'>total approvals: {BigNumber.from(request[4]).toNumber()}</p>
                                    <p className='py-4'>total depositor: {project.totalDepositors}</p><div className='sm:grid sm:grid-cols-1 xs:grid xs:grid-cols-1'>
                                        <button onClick={() => approveRequest(request, projectID)} className="bg-white text-black rounded-md my-10 mx-1 px-3 py-2 shadow-lg border-2">Approve</button><button onClick={() => rejectRequest(request, projectID)} className="bg-white text-black rounded-md my-10 px-3 mx-1 py-2 shadow-lg border-2">Reject</button><button onClick={() => transferFunds(request, projectID)} className="bg-white text-black rounded-md my-10 px-3 mx-1 py-2 shadow-lg border-2">Withdraw</button>
                                    </div>
                                </div>
                            </div>
                        )
                    }
                </div>
            </div>
        </div >
    )
}export async function getStaticPaths() {
    let provider = new ethers.providers.JsonRpcProvider(`[https://rinkeby.infura.io/v3/${infuraKey}`](https://rinkeby.infura.io/v3/${infuraKey}`))// localhost
    // let provider = new ethers.providers.JsonRpcProvider()vvvvv
    const contract = new ethers.Contract(contractAddress, CrowdFund.abi, provider)
    const data = await contract.getAllProjects()// populate the dynamic routes with the id
    const paths = data.map(d => ({ params: { id: BigNumber.from(d[0]).toString() } }))return {
        paths,
        fallback: true
    }
}// local fetch - change to ropsten/mainnet on deployement time
export async function getStaticProps({ params }) {
    // isolate ID from params
    const { id } = params// contact the blockchain
    let provider = new ethers.providers.JsonRpcProvider(`[https://rinkeby.infura.io/v3/${infuraKey}`](https://rinkeby.infura.io/v3/${infuraKey}`))// localhost
    // let provider = new ethers.providers.JsonRpcProvider()const contract = new ethers.Contract(contractAddress, CrowdFund.abi, provider)
    const data = await contract.getProjectDetails(id);// parse received data into JSON
    let projectData = {
        creator: data.creator,
        name: data.name,
        description: data.description,
        projectDeadline: BigNumber.from(data.projectDeadline).toNumber(),
        totalPledged: ethers.utils.formatEther(data.totalPledged),
        goal: ethers.utils.formatEther(data.goal),
        totalDepositors: BigNumber.from(data.totalDepositors).toNumber(),
        totalWithdrawn: ethers.utils.formatEther(data.totalWithdrawn),
        currentState: data.currentState
    }// return JSON data belonging to this route
    return {
        props: {
            project: projectData,
            projectID: id
        },
    }
}
```

最后，我们为不存在的路由创建一个 404 页面。在 pages 目录中创建一个名为 404.js 的文件

```
const notFound = () => {
  return (
    <div className='flex h-screen'>
        <p className='m-auto'>404 Not Found</p>
    </div>
  )
}export default notFound
```

这就完成了代码。奔跑

```
yarn build
```

创建优化的版本。推送到 github，部署到 vercel，你就有了一个随时可以交互的 dapp。

我希望你能从中受益。如果你有，请帮助你的孩子

(ETH)0xf 1128 dff 5816 f 80241 d6e 7 de 4 F3 cc 5b 5 E4 C5 a 819

或者

(BTC)1e8gcslrzqfbzuxcpsodbg 8 xuv 6 GX ark

直到下一次🖖

> *加入 Coinmonks* [*电报频道*](https://t.me/coincodecap) *和* [*Youtube 频道*](https://www.youtube.com/c/coinmonks/videos) *了解加密交易和投资*

# 另外，阅读

*   [Bookmap 点评](https://coincodecap.com/bookmap-review-2021-best-trading-software) | [美国 5 大最佳加密交易所](https://coincodecap.com/crypto-exchange-usa)
*   最佳加密[硬件钱包](/coinmonks/hardware-wallets-dfa1211730c6) | [Bitbns 评论](/coinmonks/bitbns-review-38256a07e161)
*   [新加坡十大最佳加密交易所](https://coincodecap.com/crypto-exchange-in-singapore) | [购买 AXS](https://coincodecap.com/buy-axs-token)
*   [红狗赌场评论](https://coincodecap.com/red-dog-casino-review) | [Swyftx 评论](https://coincodecap.com/swyftx-review) | [CoinGate 评论](https://coincodecap.com/coingate-review)
*   [投资印度的最佳密码](https://coincodecap.com/best-crypto-to-invest-in-india-in-2021)|[WazirX P2P](https://coincodecap.com/wazirx-p2p)|[Hi Dollar Review](https://coincodecap.com/hi-dollar-review)