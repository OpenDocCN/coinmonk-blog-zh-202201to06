# 加密:使用 Python 发送和管理特殊订单类型

> 原文：<https://medium.com/coinmonks/crypto-send-manage-special-order-types-using-python-3d3731900ef5?source=collection_archive---------4----------------------->

除了常用的限价、市价和止损订单类型，FTX 等加密交易所还支持更长的订单类型列表，如其网站[所述](https://help.ftx.com/hc/en-us/articles/360031896592-Advanced-Order-Types)。本文将介绍如何在**算法交易**中发送和管理这些不同的订单类型。

*   限制
*   市场
*   止损(限额和市场)
*   止盈(限价和市价)
*   跟踪止损
*   重试，直到填满