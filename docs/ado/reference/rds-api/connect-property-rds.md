---
title: Connect 屬性（RDS） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0f89e1097565c5b9841db69ac44e13c8d7138e64
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82755590"
---
# <a name="connect-property-rds"></a>Connect 屬性 (RDS)
表示執行查詢和更新作業的資料庫名稱。  
  
 在設計階段，您可以在 RDS 中設定**連接**屬性[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的物件標記，或在腳本程式碼中的執行時間（例如 VBScript）。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 有效的連接字串。 如需連接字串的一般資訊，請參閱[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性或您的提供者檔。  
  
> [!NOTE]
>  指定 MS Remote 做為 RDS 的提供者 **。DataControl**會建立一個四層案例。 超過三層的案例尚未經過測試，因此不需要使用。  
  
 *DataControl*  
 代表 RDS 的物件變數 **。DataControl**物件。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [Connect 屬性範例（VBScript）](../../../ado/reference/rds-api/connect-property-example-vbscript.md)   
 [Query 方法（RDS）](../../../ado/reference/rds-api/query-method-rds.md)   
 [Refresh 方法（RDS）](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


