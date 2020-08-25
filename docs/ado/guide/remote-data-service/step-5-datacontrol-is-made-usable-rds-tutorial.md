---
description: 步驟 5：將 DataControl 設為可用 (RDS 教學課程)
title: 步驟5： DataControl 可用 (RDS 教學課程) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], datacontrol made usable
ms.assetid: ed5c4a24-9804-4c85-817e-317652acb9b4
author: rothja
ms.author: jroth
ms.openlocfilehash: 616b82b397694e4db41f709080dc4beafd945878
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759018"
---
# <a name="step-5-datacontrol-is-made-usable-rds-tutorial"></a>步驟 5：將 DataControl 設為可用 (RDS 教學課程)
傳回的 **記錄集** 物件可供使用。 您可以檢查、流覽或編輯它，就像任何其他 **記錄集**一樣。 您可以使用 **記錄集** 來做些什麼，取決於您的環境。 Visual Basic 和 Visual C++ 具有視覺控制項，可透過啟用資料控制的輔助來直接或間接使用 **記錄集** 。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 例如，如果您要在 Microsoft Internet Explorer 中顯示網頁，您可能會想要在視覺化控制項中顯示 **記錄集** 物件資料。 網頁上的視覺控制項無法直接存取 **記錄集** 物件。 不過，他們可以透過 RDS 存取 **記錄集** 物件 [。DataControl](../../reference/rds-api/datacontrol-object-rds.md)。 **RDS。** 當視覺控制項的[SourceRecordset](../../reference/rds-api/recordset-sourcerecordset-properties-rds.md)屬性設定為**記錄集**物件時，DataControl 就會變成可供使用。  
  
 視覺化控制項物件的 **DATASRC** 參數必須設定為 **RDS。DataControl**，並將其 **DATAFLD** 屬性設定為 **記錄集** 物件欄位， (資料行) 。  
  
 在本教學課程中，請設定 **SourceRecordset** 屬性：  
  
```vb
Sub RDSTutorial5()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DC as New RDS.DataControl  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
   DC.SourceRecordset = RS         ' Visual controls can now bind to DC.  
...  
```  
  
## <a name="see-also"></a>另請參閱  
 [步驟6：將變更傳送到伺服器 (RDS 教學課程) ](./step-6-changes-are-sent-to-the-server-rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](./rds-tutorial-vbscript.md)