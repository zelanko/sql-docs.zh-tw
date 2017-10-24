---
title: "查詢方法 (RDS) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Query method [ADO]
ms.assetid: 20f2480f-3758-405d-a379-05a0dce74796
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 53647d80b2e6110e5af084e6a3f983381ced1690
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="query-method-rds"></a>查詢方法 (RDS)
使用有效的 SQL 查詢字串傳回[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set Recordset = DataFactory.Query(Connection, Query)  
```  
  
#### <a name="parameters"></a>參數  
 *資料錄集*  
 物件變數，表示**資料錄集**物件。  
  
 *DataFactory*  
 物件變數，表示[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件。  
  
 *連接*  
 A**字串**包含伺服器連接資訊的值。 這是類似於[連接](../../../ado/reference/rds-api/connect-property-rds.md)屬性。  
  
 *查詢*  
 A**字串**，其中包含 SQL 查詢。  
  
## <a name="remarks"></a>備註  
 查詢應該使用資料庫伺服器的 SQL 的用語。 如果發生錯誤的查詢來執行，則傳回結果狀態。 **查詢**方法不會執行任何語法上檢查**查詢**字串。  
  
## <a name="applies-to"></a>適用於  
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataFactory 物件、 查詢方法和 CreateObject 方法範例 (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)



