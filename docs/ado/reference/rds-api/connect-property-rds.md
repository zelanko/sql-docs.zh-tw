---
title: 連接屬性 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Connect property [ADO]
ms.assetid: dbad5e77-b213-4eb8-aecf-d60f203fdb59
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba8b5aa1f59fbb161da878f5930f83d2f6ff0bdd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964569"
---
# <a name="connect-property-rds"></a>Connect 屬性 (RDS)
指出從中執行的查詢和更新作業的資料庫名稱。  
  
 您可以設定**Connect**屬性，在設計階段於[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的物件標記，或在指令碼 (例如，VBScript) 中的執行階段。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 有效的連接字串。 更多一般連接字串的詳細資訊，請參閱[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性或您的提供者文件。  
  
> [!NOTE]
>  指定做為提供者的 MS 遠端**rds。DataControl**會建立四個層的案例。 大於三個層級的案例尚未經過測試，並不需要。  
  
 *DataControl*  
 物件變數，表示**rds。DataControl**物件。  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [Connect 屬性範例 (VBScript)](../../../ado/reference/rds-api/connect-property-example-vbscript.md)   
 [查詢方法 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Refresh 方法 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


