---
description: RDS 方法
title: RDS 方法 |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
helpviewer_keywords:
- RDS methods [ADO]
- methods [ADO], RDS
ms.assetid: c2c6af1a-3c44-4c9d-ad33-b381552c71af
author: rothja
ms.author: jroth
ms.openlocfilehash: 3403fa1baeeaa2c5e09f3b3f3e116325ecaef77c
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767747"
---
# <a name="rds-methods"></a>RDS 方法
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
|方法|描述|  
|-|-|  
|[取消 (RDS) ](./cancel-method-rds.md)|取消執行暫止的非同步方法呼叫。|  
|[CancelUpdate (RDS) ](./cancelupdate-method-rds.md)|取消對 **記錄集** 物件的目前或新資料列所做的任何變更。|  
|[ConvertToString (RDS) ](./converttostring-method-rds.md)|將 **記錄集** 轉換為代表記錄集資料的 MIME 字串。|  
|[CreateObject (RDS) ](./createobject-method-rds.md)|建立目標商務物件的 proxy，並傳回其指標。|  
|[CreateRecordset (RDS) ](./createrecordset-method-rds.md)|建立空白、中斷連接的 **記錄集**。|  
|[Execute 方法 (RDS)](./execute-method-rds.md)|執行要求，並建立「advanced data 資料列集」 (以用於 ADO 2.5 和更新版本的) 。|  
|[Execute21 方法 (RDS)](./execute21-method-rds.md)|執行要求，並建立「advanced data 資料列集」 (以用於 ADO 2.1) 。|  
|[InvokeService (RDS)](./invokeservice-rds.md)|在更強大的物件版本上，將指標傳回至要求的介面。|  
|[MoveFirst、MoveLast、MoveNext、MovePrevious (RDS) ](./movefirst-movelast-movenext-and-moveprevious-methods-rds.md)|移至指定之 **記錄集** 物件中的第一個、最後一個、下一個或上一個記錄。|  
|[ (RDS) 的查詢 ](./query-method-rds.md)|使用有效的 SQL 查詢字串來傳回 **記錄集**。|  
|[ (RDS) 重新整理 ](./refresh-method-rds.md)|重新查詢 **Connect** 屬性中指定的資料來源，並更新查詢結果。|  
|[重設 (RDS) ](./reset-method-rds.md)|根據指定的排序和篩選屬性，執行用戶端 **記錄集**的排序或篩選。|  
|[SubmitChanges (RDS) ](./submitchanges-method-rds.md)|將本機快取和可更新 **記錄集** 的暫止變更提交至 **Connect** 屬性中指定的資料來源。|  
|[Synchronize 方法 (RDS)](./synchronize-method-rds.md)|將指定的記錄集與連接字串所指定的資料庫同步處理 (，以用於 ADO 2.5 和更新版本的) 。|  
|[Synchronize21 方法 (RDS)](./synchronize21-method-rds.md)|將指定的記錄集與連接字串所指定的資料庫同步處理 (以便與 ADO 2.1) 搭配使用。|