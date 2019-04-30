---
title: 取得描述項會處理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 983097de95e41914bb4d577cb071d790a795f96d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63254681"
---
# <a name="obtaining-descriptor-handles"></a>取得描述項控制代碼
應用程式當做輸出引數的呼叫中取得的任何明確配置描述項控制代碼**SQLAllocHandle**。 藉由呼叫取得的隱含配置描述項控制代碼**SQLGetStmtAttr**。
