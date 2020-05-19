---
title: Query 方法（RDS） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b3025f37b47cd545e7e7cde127e96740077ab961
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82751501"
---
# <a name="query-method-rds"></a>Query 方法 (RDS)
使用有效的 SQL 查詢字串來傳回[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set Recordset = DataFactory.Query(Connection, Query)  
```  
  
#### <a name="parameters"></a>參數  
 *Recordset*  
 代表**記錄集**物件的物件變數。  
  
 *DataFactory*  
 代表[RDSServer DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件的物件變數。  
  
 *建立*  
 包含伺服器連接資訊的**字串**值。 這類似于[Connect](../../../ado/reference/rds-api/connect-property-rds.md)屬性。  
  
 *查詢*  
 包含 SQL 查詢的**字串**。  
  
## <a name="remarks"></a>備註  
 查詢應該使用資料庫伺服器的 SQL 方言。 如果已執行的查詢發生錯誤，則會傳回結果狀態。 **查詢**方法不會對**查詢**字串執行任何語法檢查。  
  
## <a name="applies-to"></a>套用至  
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataFactory 物件、Query 方法和 CreateObject 方法範例 (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


