---
description: 在 Visual Basic 6 應用程式中參考 ADO 程式庫
title: 在 Visual Basic 6 應用程式中參考 ADO 程式庫 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual Basic application[ADO]
- ADO, libraries
ms.assetid: cfd37a82-aad2-41cd-8d13-1566c43d95f0
author: rothja
ms.author: jroth
ms.openlocfilehash: 71ae81dc98d0fffe7463759be0846afccd708f0f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978509"
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>在 Visual Basic 6 應用程式中參考 ADO 程式庫
若要將 ADO 程式庫匯入到 Microsoft Visual Basic 6 應用程式中，您必須在 Visual Basic 專案中設定參考。  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>若要在 Visual Basic 專案中設定 ADO 程式庫的參考  
  
1.  建立新的或開啟現有的 Visual Basic 專案。  
  
2.  按一下 [ **專案** ] 功能表項目，然後從下拉式功能表面板中選取 [ **參考 ...** ]。  
  
3.  從 [ **可用的參考**] 中，核取 [ **Microsoft ActiveX Data Objects *n-1* **] 程式庫，其中 ***n. n*** 表示最新的版本號碼。 下列 **位置** 欄位應該將您的選擇識別為 *$installDir\msado15.dll*，其中 *$installDir* 代表已安裝 ADO 程式庫的目錄路徑。  
  
4.  如果您想要使用 ADO MD，請重複步驟3以選取 [ **Microsoft ActiveX Data Objects (多維度) *n. n* 程式庫**]。 [ **位置** ] 欄位應該將此選項識別為 *$installDir\msadomd.dll*。  
  
5.  如果您想要使用 ADOX，請重複步驟3，為**DDL 和安全性*n.n*選取 Microsoft ADO Ext.** n。 [ **位置** ] 欄位應該將此選項識別為 *$installDir\msadox.dll*。  
  
6.  按一下 **[確定** ] 完成設定參考。  
  
## <a name="backward-compatibility"></a>回溯相容性  
 安裝 ADO 也會複製下列舊版的類型程式庫：  
  
-   *msado27 .tlb*、ADO 2.7 類型程式庫  
  
-   *msado26 .tlb*、ADO 2.6 類型程式庫  
  
-   *msado25 .tlb*、ADO 2.5 類型程式庫  
  
-   *msado21 .tlb*、ADO 2.1 類型程式庫  
  
-   *msado20 .tlb*、ADO 2.0 類型程式庫  
  
 如果您的應用程式必須基於回溯相容性的原因，使用上述任何 ADO 程式庫，您必須匯入適當版本的類型程式庫。 若要這樣做，請遵循上一節中的程式，以*msadoXX*取代*msado15.dll* ，其中*XX*代表您需要匯入的版本號碼。
