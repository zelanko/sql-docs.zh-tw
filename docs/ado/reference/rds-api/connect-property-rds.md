---
title: "連接屬性 (RDS) |Microsoft 文件"
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
- Connect property [ADO]
ms.assetid: dbad5e77-b213-4eb8-aecf-d60f203fdb59
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 46668b0b90099994724e39dc5f9d911431e6fd85
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="connect-property-rds"></a>屬性 (RDS) 連接
表示要從中執行的查詢和更新作業的資料庫名稱。  
  
 您可以設定**連接**屬性在設計階段於[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的物件標記，或在執行階段於指令碼 (例如，VBScript)。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>參數  
 *連接字串*  
 有效的連接字串。 一般連接字串的詳細資訊，請參閱[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性或您的提供者文件。  
  
> [!NOTE]
>  指定做為提供者的 MS 遠端**.RDSDataControl**會建立四個層案例。 案例三個層級大於尚未經過測試，並不需要。  
  
 *DataControl*  
 物件變數，表示**.RDSDataControl**物件。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [連接屬性的範例 (VBScript)](../../../ado/reference/rds-api/connect-property-example-vbscript.md)   
 [查詢方法 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [重新整理方法 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)



