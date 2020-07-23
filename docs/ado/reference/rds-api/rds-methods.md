---
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
ms.openlocfilehash: c178bae1f3da5ccc6ca4cfdd6b5645335141908f
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942300"
---
# <a name="rds-methods"></a>RDS 方法
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
|方法|描述|  
|-|-|  
|[取消（RDS）](../../../ado/reference/rds-api/cancel-method-rds.md)|取消執行暫止的非同步方法呼叫。|  
|[CancelUpdate （RDS）](../../../ado/reference/rds-api/cancelupdate-method-rds.md)|取消對**記錄集**物件的目前或新資料列所做的任何變更。|  
|[ConvertToString （RDS）](../../../ado/reference/rds-api/converttostring-method-rds.md)|將**記錄集**轉換成代表記錄集資料的 MIME 字串。|  
|[CreateObject （RDS）](../../../ado/reference/rds-api/createobject-method-rds.md)|建立目標商務物件的 proxy，並傳回它的指標。|  
|[CreateRecordset （RDS）](../../../ado/reference/rds-api/createrecordset-method-rds.md)|建立空的、中斷連接的**記錄集**。|  
|[Execute 方法 (RDS)](../../../ado/reference/rds-api/execute-method-rds.md)|執行要求並建立 advanced data 資料列集（以用於 ADO 2.5 和更新版本）。|  
|[Execute21 方法 (RDS)](../../../ado/reference/rds-api/execute21-method-rds.md)|執行要求並建立 advanced data 資料列集（以用於 ADO 2.1）。|  
|[InvokeService (RDS)](../../../ado/reference/rds-api/invokeservice-rds.md)|在物件的支援版本上，傳回所要求介面的指標。|  
|[MoveFirst、MoveLast、MoveNext、MovePrevious （RDS）](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)|移至指定之**記錄集**物件中的第一個、最後一個、下一個或上一個記錄。|  
|[查詢（RDS）](../../../ado/reference/rds-api/query-method-rds.md)|使用有效的 SQL 查詢字串來傳回**記錄集**。|  
|[Refresh （RDS）](../../../ado/reference/rds-api/refresh-method-rds.md)|重新查詢**連接**屬性中所指定的資料來源，並更新查詢結果。|  
|[重設（RDS）](../../../ado/reference/rds-api/reset-method-rds.md)|根據指定的排序和篩選屬性，在用戶端**記錄集**上執行排序或篩選。|  
|[SubmitChanges （RDS）](../../../ado/reference/rds-api/submitchanges-method-rds.md)|將本機快取和可更新**記錄集**的暫止變更提交至**連接**屬性中所指定的資料來源。|  
|[Synchronize 方法 (RDS)](../../../ado/reference/rds-api/synchronize-method-rds.md)|將指定的記錄集與連接字串所指定的資料庫同步處理（以用於 ADO 2.5 和更新版本）。|  
|[Synchronize21 方法 (RDS)](../../../ado/reference/rds-api/synchronize21-method-rds.md)|將指定的記錄集與連接字串所指定的資料庫同步處理（以用於 ADO 2.1）。|


