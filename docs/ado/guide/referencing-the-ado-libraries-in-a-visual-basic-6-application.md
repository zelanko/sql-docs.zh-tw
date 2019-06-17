---
title: 參考 ADO 程式庫中的 Visual Basic 6 應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual Basic application[ADO]
- ADO, libraries
ms.assetid: cfd37a82-aad2-41cd-8d13-1566c43d95f0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 80385161bcfce2c4b39ec9fa1257358cabe5f98c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704374"
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>在 Visual Basic 6 應用程式中參考 ADO 程式庫
ADO 程式庫匯入的 Microsoft Visual Basic 6 應用程式，您必須在 Visual Basic 專案中設定的參考。  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>若要設定 Visual Basic 專案中的 ADO 程式庫的參考  
  
1.  建立新的或開啟現有的 Visual Basic 專案。  
  
2.  按一下 [**專案**功能表項目，然後選取**參考...** 從下拉式選單] 面板。  
  
3.  從 **可用的參考** ，核取方塊 **Microsoft ActiveX Data Objects *n.n* 文件庫** ，其中 ***n.n*** 代表最新版本號碼。 **位置**下方的欄位應該識別為自選 *$installDir\msado15.dll*，其中 *$installDir*表示在其中的目錄路徑的 ADO 程式庫已安裝。  
  
4.  如果您想要使用 ADO MD，重複步驟 3 選取 **（多維度） 的 Microsoft ActiveX Data Objects *n.n*程式庫**。 **位置**欄位應該識別這項選擇作為 *$installDir\msadomd.dll*。  
  
5.  如果您想要使用 ADOX，重複步驟 3 選取 **Microsoft ADO 分機 *n.n* DDL 和安全性** 。 **位置**欄位應該識別這項選擇作為 *$installDir\msadox.dll*。  
  
6.  按一下 **確定**完成設定的參考。  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 安裝 ADO 時，也會複製舊版本的下列類型程式庫：  
  
-   *msado27.tlb*，ADO 2.7 的型別程式庫  
  
-   *msado26.tlb*，ADO 2.6 的型別程式庫  
  
-   *msado25.tlb*，ADO 2.5 的型別程式庫  
  
-   *msado21.tlb*，ADO 2.1 的型別程式庫  
  
-   *msado20.tlb*，ADO 2.0 類型程式庫  
  
 如果您的應用程式必須使用任何這些 ADO 程式庫的回溯相容性的原因，您需要匯入適當的型別程式庫版本。 若要這樣做，請遵循上一節中的程序取代*msado15.dll*依*msadoXX.tlb*，其中*XX*代表您要匯入的版本號碼。
