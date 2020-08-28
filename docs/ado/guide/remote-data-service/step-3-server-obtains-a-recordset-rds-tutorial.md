---
description: 步驟 3：伺服器取得資料錄集 (RDS 教學課程)
title: 步驟3：伺服器取得記錄集 (RDS 教學課程) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], server obtains Recordset
ms.assetid: 9c6779c9-1208-4696-ac51-c39f3a6d9240
author: rothja
ms.author: jroth
ms.openlocfilehash: 494cf7a3be5206f5fd4f89d3f575989ce51002b9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977539"
---
# <a name="step-3-server-obtains-a-recordset-rds-tutorial"></a>步驟 3：伺服器取得資料錄集 (RDS 教學課程)
伺服器程式會使用連接字串和命令文字來查詢資料來源中所需的資料列。 ADO 通常用來抓取此 **記錄集**，不過可以使用其他 Microsoft 資料存取介面（例如 OLE DB）。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 自訂伺服器程式可能如下所示：  
  
```vb
Public Function ServerProgram(cn as String, qry as String) as Object  
Dim rs as New ADODB.Recordset  
   rs.CursorLocation = adUseClient  
   rs.Open qry, cn   
   rs.ActiveConnection = Nothing  
   Set ServerProgram = rs  
End Function  
```  
  
## <a name="see-also"></a>另請參閱  
 [步驟4：伺服器傳回記錄集 (RDS 教學課程) ](./step-4-server-returns-the-recordset-rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](./rds-tutorial-vbscript.md)