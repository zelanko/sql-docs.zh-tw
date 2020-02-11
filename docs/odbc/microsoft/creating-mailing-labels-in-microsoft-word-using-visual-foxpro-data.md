---
title: 使用 Visual FoxPro 資料在 Microsoft Word 中建立郵件標籤 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data [ODBC], mailing labels
- Visual FoxPro data [ODBC], Word
- mailing labels [ODBC]
- Visual FoxPro ODBC driver [ODBC], Word
- FoxPro ODBC driver [ODBC], word
ms.assetid: c901b60c-9f84-407a-b3d1-b4d301a71370
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 73880171493555a7d30e5c0c5419d02338961e9b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096519"
---
# <a name="creating-mailing-labels-in-microsoft-word-using-visual-foxpro-data"></a>使用 Visual FoxPro 資料在 Microsoft Word 中建立郵件標籤
您可以在 Windows 95 或 Windows 98 檔的 Microsoft Word 中使用 Visual FoxPro 資料。 例如，您可能會想要從儲存在 Visual FoxPro 資料表中的客戶資訊建立郵寄標籤。  
  
### <a name="to-create-mailing-labels"></a>建立郵件標籤  
  
1.  在 Microsoft Word 中，建立新的空白檔。  
  
2.  從 [工具] 功能表中，選擇 [合併列印]。  
  
3.  在合併列印 Helper 中，選擇 [建立]，然後選取 [郵件標籤]。  
  
4.  在 [主要檔] 下，選擇 [使用中視窗]。  
  
5.  在 [資料來源] 底下，選擇 [取得資料]，然後選取 [開啟資料來源]。  
  
6.  在 [開啟資料來源] 對話方塊中，選擇 [MS 查詢]。  
  
7.  在 [選取資料來源] 對話方塊中，選取一個 Visual FoxPro 資料來源，然後按一下 [使用]。  
  
8.  如果資料來源存取的資料庫包含資料表，請從 [加入資料表] 對話方塊中選取資料表。 Microsoft Query 會在查詢設計工具的上半部顯示加入的資料表。  
  
9. 選取查詢的欄位，方法是將其從資料表拖曳至設計工具的下半部。  
  
10. 從 [檔案] 功能表中，選擇 [將資料傳回給 Microsoft Word]。 Microsoft Query 會關閉，而您選取的資料可用於合併列印檔。  
  
11. 在 [主要檔] 下，選擇 [設定]。  
  
12. 在 [標籤選項] 對話方塊中，選取您想要的印表機和標籤資訊，然後按一下 [確定]。  
  
13. 在 [建立標籤] 對話方塊中，選取您想要在郵件標籤上列印的欄位，然後按一下 [確定]。  
  
14. 在 [合併列印協助程式] 中的 [與檔合併資料] 底下，按一下 [合併]。  
  
15. 在 [合併] 對話方塊中，選取您想要的選項，然後按一下 [合併]。
