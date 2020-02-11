---
title: 在 Visual Basic 6 應用程式中參考 ADO 程式庫 |Microsoft Docs
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
ms.openlocfilehash: 25ea858995c884af202d3d80f4de675c9f4cda27
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923054"
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>在 Visual Basic 6 應用程式中參考 ADO 程式庫
若要將 ADO 程式庫匯入 Microsoft Visual Basic 6 應用程式，您必須在 Visual Basic 專案中設定參考。  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>若要在 Visual Basic 專案中設定 ADO 程式庫的參考  
  
1.  建立新的或開啟現有的 Visual Basic 專案。  
  
2.  按一下 [**專案**] 功能表項目，然後從下拉式功能表面板中選取 [**參考 ...** ]。  
  
3.  從 [**可用的參考**] 中，核取 [ **Microsoft ActiveX Data Objects *n. n* **] 程式庫的方塊，其中***n. n***代表最新的版本號碼。 下方的 [**位置**] 欄位應該將您的選擇識別為 *$installDir \msado15.dll*，其中 *$installDir*代表已安裝 ADO 程式庫的目錄路徑。  
  
4.  如果您想要使用 ADO MD，請重複步驟3以選取 **[Microsoft ActiveX Data Objects （多維度）] [ *n* **] 程式庫。 [**位置**] 欄位應該將此選擇識別為 *$installDir \msadomd.dll*。  
  
5.  如果您想要使用 ADOX，請重複步驟3，**針對 DDL 和安全性** 選取 [Microsoft ADO Ext**]。 [**位置**] 欄位應該將此選擇識別為 *$installDir \msadox.dll*。  
  
6.  按一下 **[確定**] 以完成參考的設定。  
  
## <a name="backward-compatibility"></a>回溯相容性  
 安裝 ADO 也會複製舊版的下列類型程式庫：  
  
-   *msado27 .tlb*、ADO 2.7 類型程式庫  
  
-   *msado26 .tlb*、ADO 2.6 類型程式庫  
  
-   *msado25 .tlb*、ADO 2.5 類型程式庫  
  
-   *msado21 .tlb*、ADO 2.1 類型程式庫  
  
-   *msado20 .tlb*、ADO 2.0 類型程式庫  
  
 如果您的應用程式因為回溯相容性的緣故而必須使用上述任何 ADO 程式庫，您必須匯入適當版本的類型程式庫。 若要這麼做，請遵循上一節中的程式，將*msado15.dll*取代為*MsadoXX*，其中*XX*代表您需要匯入的版本號碼。
