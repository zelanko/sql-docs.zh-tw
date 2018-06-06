---
title: HelloData： 簡單的 ADO 應用程式 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- HelloData sample application [ADO]
- ADO, samples
ms.assetid: de4bcd56-dac2-45e6-95ab-9fd7f25878fc
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3fbc270a27350160933019c16c3b354270beb64f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="hellodata-a-simple-ado-application"></a>HelloData： 簡單的 ADO 應用程式
這個簡單的應用程式逐步執行每四個主要的 ADO 作業： 取得、 檢視、 編輯和更新的資料。 這些作業將會對 Microsoft® SQL Server 隨附 Northwind 範例資料庫。 若要將焦點放在 ADO 的基本概念，並防止程式碼雜亂，此範例中的錯誤處理是最小。  
  
### <a name="to-run-hellodata"></a>若要執行 HelloData  
  
1.  建立新的標準 EXE Visual Basic 專案參考 ADO 程式庫。 如需詳細資訊，請參閱[參考 ADO 庫](../../../ado/guide/referencing-the-ado-libraries.md)。  
  
2.  建立四個命令按鈕上方的表單，並設定**名稱**和**標題**屬性在本主題結尾的資料表中所顯示的值。  
  
3.  下方的按鈕，加入**Microsoft DataGrid 控制項**(Msdatgrd.ocx)。 Msdatgrd.ocx 檔案隨附於 Visual Basic，而且位於 \windows\system32 或 \winnt\system32 目錄中。 若要加入 Visual Basic 的 [工具箱] 窗格中的 DataGrid 控制項，請選取**元件...** 從**專案**功能表。 旁邊核取方塊"Microsoft DataGrid 控制項 6.0 (SP3) (OLEDB) 」，然後按一下 **確定**。 若要將控制項加入至專案，DataGrid 控制項從工具箱拖曳至 Visual Basic 表單。  
  
4.  建立**文字方塊**表單下方方格上並設定其屬性，如下表所示。 當您完成時，表單應該類似下圖。  
  
5.  最後，將複製程式碼中所列[HelloData 程式碼](../../../ado/guide/data/hellodata-code.md)，並將它貼到表單的程式碼編輯器視窗。 按**F5**執行的程式碼。  
  
> [!NOTE]
>  在下列範例中，而且指南，"MyId 「 密碼 」 123aBc"的使用者識別碼用來對伺服器進行驗證。 您應該為您的伺服器取代具有有效的登入認證這些值。 此外，取代"MySQLServer"的值與您的伺服器名稱。  
  
 如需程式碼的詳細說明，請參閱[HelloData 的註解](../../../ado/guide/data/comments-on-hellodata.md)。  
  
 ![顯示 HelloData VB 應用程式的 Form1](../../../ado/guide/data/media/hellodata.gif "HelloData")  
  
|控制項類型|屬性|Value|  
|------------------|--------------|-----------|  
|表單|名稱|Form1|  
||高度|6500|  
||寬度|6500|  
|MS DataGrid|名稱|grdDisplay1|  
|TextBox|名稱|txtDisplay1|  
||多行|true|  
|命令按鈕|名稱|cmdGetData|  
||Caption|取得資料|  
|命令按鈕|名稱|cmdExamineData|  
||Caption|檢查資料|  
|命令按鈕|名稱|cmdEditData|  
||Caption|編輯資料|  
|命令按鈕|名稱|cmdUpdateData|  
||Caption|更新資料|
