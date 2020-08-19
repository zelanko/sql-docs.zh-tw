---
description: Connect 屬性 (RDS)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: eb3b5e535d2f4b6f6e4777c8c3ac1bbaaa3381c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439210"
---
# <a name="connect-property-rds"></a>Connect 屬性 (RDS)
指出執行查詢和更新作業的資料庫名稱。  
  
 您可以在 RDS 的設計階段設定 **連接** 屬性 [。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 物件的物件標記，或在執行時間的腳本程式碼 (例如，VBScript) 。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>參數  
 *ConnectionString*  
 有效的連接字串。 如需連接字串的一般資訊，請參閱 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 屬性或您的提供者檔。  
  
> [!NOTE]
>  指定 MS Remote 作為 RDS 的提供者 **。DataControl** 會建立四層案例。 超過三個層級的案例尚未經過測試，因此不需要。  
  
 *DataControl*  
 代表 RDS 的物件變數 **。DataControl** 物件。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VBScript) 的連接屬性範例 ](../../../ado/reference/rds-api/connect-property-example-vbscript.md)   
 [ (RDS) 的查詢方法 ](../../../ado/reference/rds-api/query-method-rds.md)   
 [ (RDS) 的 Refresh 方法 ](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


