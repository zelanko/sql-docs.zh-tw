---
description: 步驟 4：伺服器傳回資料錄集 (RDS 教學課程)
title: 步驟4：伺服器傳回記錄集 (RDS 教學課程) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], server returns Recordset
ms.assetid: 3d1855c4-419c-4810-b5ea-6c874b5e2905
author: rothja
ms.author: jroth
ms.openlocfilehash: 80db98699916cea22cd2815871f99159b1f1a7c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451920"
---
# <a name="step-4-server-returns-the-recordset-rds-tutorial"></a>步驟 4：伺服器傳回資料錄集 (RDS 教學課程)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 RDS 會將抓取的**記錄集**物件轉換成可以傳送回用戶端的表單 (也就是說，它會將**記錄集***封送*處理) 。 轉換的確切形式和其傳送方式，取決於伺服器是在網際網路或內部網路、區域網路或動態連結程式庫。 不過，這項詳細資料並不重要;最重要的是，RDS 會將 **記錄集** 傳回給用戶端。  
  
 在用戶端上，會傳回 **記錄集** 物件，並將其指派給本機變數。  
  
```vb
Sub RDSTutorial4()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>另請參閱  
 [步驟5： DataControl 可用 (RDS 教學課程) ](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
