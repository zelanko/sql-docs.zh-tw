---
title: 步驟 3：伺服器會取得資料錄集 （RDS 教學課程） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], server obtains Recordset
ms.assetid: 9c6779c9-1208-4696-ac51-c39f3a6d9240
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: eb0afbbe470a1cc9cddbf9e9f2f892deb7ce0864
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704162"
---
# <a name="step-3-server-obtains-a-recordset-rds-tutorial"></a>步驟 3：伺服器會取得資料錄集 (RDS 教學課程)
伺服器程式會使用連接字串和命令文字，來查詢所需的資料列的資料來源。 ADO 通常用來擷取這**資料錄集**，不過，其他 Microsoft 資料存取介面，例如 OLE DB 中，無法使用。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 自訂伺服器程式可能看起來像這樣：  
  
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
 [步驟 4：伺服器會傳回資料錄集 （RDS 教學課程）](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
