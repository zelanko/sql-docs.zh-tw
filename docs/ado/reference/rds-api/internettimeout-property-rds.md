---
description: InternetTimeout 屬性 (RDS)
title: InternetTimeout 屬性 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InternetTimeout property [ADO]
ms.assetid: 4d1c8892-4bbc-4e71-bf4b-ba52c0ea9549
author: rothja
ms.author: jroth
ms.openlocfilehash: 9dbc94caa6266ff2f44a07c8792ff8b6287fd61c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438920"
---
# <a name="internettimeout-property-rds"></a>InternetTimeout 屬性 (RDS)
表示要求超時前等待的毫秒數。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **Long** 值，表示要求超時之前的毫秒數。  
  
## <a name="remarks"></a>備註  
 這個屬性只適用于以 HTTP 或 HTTPS 通訊協定傳送的要求。  
  
 在三層環境中的要求可能需要幾分鐘的時間來執行。 您可以使用這個屬性來指定長時間執行之要求的額外時間。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
    :::column-end:::
    :::column:::
        [DataSpace 物件 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [ (VB) 的 InternetTimeout 屬性範例 ](../../../ado/reference/rds-api/internettimeout-property-example-vb.md)   
 [InternetTimeout 屬性範例 (VC++)](../../../ado/reference/rds-api/internettimeout-property-example-vc.md)   
 

