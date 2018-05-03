---
title: 參考 Visual Basic 6 應用程式中的 ADO 程式庫 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology: drivers
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual Basic application[ADO]
- ADO, libraries
ms.assetid: cfd37a82-aad2-41cd-8d13-1566c43d95f0
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 745e305dc6b513a22bce48b40f511a850386e1b4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>參考 Visual Basic 6 應用程式中的 ADO 程式庫
ADO 程式庫匯入的 Microsoft Visual Basic 6 應用程式，您必須在 Visual Basic 專案中設定參考。  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>在 Visual Basic 專案中設定 ADO 程式庫的參考  
  
1.  建立新的或開啟現有的 Visual Basic 專案。  
  
2.  按一下**專案**功能表項目，然後選取**參考...** 從下拉功能表面板。  
  
3.  從**可用的參考**，核取方塊， **Microsoft ActiveX Data Objects *n.n*文件庫**，其中***n.n***代表最新版本號碼。 **位置**下列欄位應該識別您的選擇為 *$installDir\msado15.dll*，其中 *$installDir*表示在其中的目錄路徑 ADO 程式庫已安裝。  
  
4.  如果您想要使用 ADO MD 中，重複步驟 3 以選取**Microsoft ActiveX Data Objects （多維度） *n.n*文件庫**。 **位置**欄位應該識別這項選擇做為 *$installDir\msadomd.dll*。  
  
5.  如果您想要使用 ADOX，重複步驟 3 以選取**Microsoft ADO 分機*n.n* DDL 和安全性**。 **位置**欄位應該識別這項選擇做為 *$installDir\msadox.dll*。  
  
6.  按一下**確定**完成設定的參考。  
  
## <a name="backward-compatibility"></a>回溯相容性  
 安裝 ADO 也會將複製舊版本的下列類型程式的庫：  
  
-   *msado27.tlb*，ADO 2.7 類型程式庫  
  
-   *msado26.tlb*，ADO 2.6 類型程式庫  
  
-   *msado25.tlb*，ADO 2.5 的型別程式庫  
  
-   *msado21.tlb*，ADO 2.1 的型別程式庫  
  
-   *msado20.tlb*，ADO 2.0 類型程式庫  
  
 如果您的應用程式必須使用任何這些 ADO 文件庫基於回溯相容性，您需要匯入類型程式庫的適當版本。 若要這樣做，請依照上一節中的程序取代*msado15.dll*由*msadoXX.tlb*，其中*XX*表示您需要匯入的版本號碼。
