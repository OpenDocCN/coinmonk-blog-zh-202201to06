# 使用 Python Websocket 从 FTX 和币安流式传输实时数据

> 原文：<https://medium.com/coinmonks/streaming-live-market-data-from-ftx-binance-using-websocket-in-python-b59a18a30cf0?source=collection_archive---------0----------------------->

对于任何在 crypto 中从事自动交易策略工作的人来说，使用 REST api 查询来自交易所的实时数据并不总是最佳实践，原因有很多:

1.  **低效率**:每个查询都需要时间，这会显著影响性能，尤其是对于高频策略。
2.  **交易所施加的限制**很容易被突破，例如【】的每分钟 1200 个请求重量的硬性限制由币安设定。
3.  只有**有限数量的历史数据**你可以…