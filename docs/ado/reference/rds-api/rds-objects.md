---
title: RDS 物件 |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
helpviewer_keywords:
- objects [ADO], RDS
- RDS objects [ADO]
ms.assetid: f2ac8b3b-f968-41c4-a504-7aee3538b7c7
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ba592cd0bb0dc10c094784fbb7d41585d5b6dd6
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942290"
---
# <a name="rds-objects"></a>RDS 物件
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
|Object|描述|  
|-|-|  
|[DataControl （RDS）](../../../ado/reference/rds-api/datacontrol-object-rds.md)|將資料查詢**記錄集**系結至一或多個控制項（例如文字方塊、方格控制項或下拉式方塊），以顯示網頁上的**記錄集**資料。<br /><br /> **DataControl**物件可安全地進行腳本處理。|  
|[DataFactory （RDSServer）](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|會執行方法，針對用戶端應用程式提供對指定資料來源的讀取/寫入資料存取。<br /><br /> 撰寫腳本時， **DataFactory**物件是不安全的。|  
|[空間（RDS）](../../../ado/reference/rds-api/dataspace-object-rds.md)|建立位於仲介層之自訂商務物件的用戶端 proxy。<br /><br /> 「**空間**」物件可安全地進行腳本處理。|  
|[IRDSService 介面 (RDS)](../../../ado/reference/rds-api/irdsservice-interface-rds.md)|公開[InvokeService （RDS）](../../../ado/reference/rds-api/invokeservice-rds.md)方法，用來在物件的支援版本上傳回所要求介面的指標。|  
  
## <a name="see-also"></a>另請參閱  
 [RDS API 參考](../../../ado/reference/rds-api/rds-api-reference.md)


