---
title: 查詢方法 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Query method [ADO]
ms.assetid: 20f2480f-3758-405d-a379-05a0dce74796
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 92247a31eeb5f3e70b54edfaff33ae15340b9df1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712430"
---
# <a name="query-method-rds"></a>Query 方法 (RDS)
會使用有效的 SQL 查詢字串傳回[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set Recordset = DataFactory.Query(Connection, Query)  
```  
  
#### <a name="parameters"></a>參數  
 *Recordset*  
 物件變數，表示**資料錄集**物件。  
  
 *DataFactory*  
 物件變數，表示[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件。  
  
 *[連接]*  
 A**字串**值，包含伺服器連接資訊。 這是類似[Connect](../../../ado/reference/rds-api/connect-property-rds.md)屬性。  
  
 *[資料集屬性]*  
 A**字串**，其中包含 SQL 查詢。  
  
## <a name="remarks"></a>備註  
 查詢應該使用資料庫伺服器的 SQL 方言。 如果使用已執行的查詢發生錯誤，則會傳回結果狀態。 **查詢**方法並不會執行任何檢查的語法**查詢**字串。  
  
## <a name="applies-to"></a>適用於  
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataFactory 物件、Query 方法和 CreateObject 方法範例 (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


