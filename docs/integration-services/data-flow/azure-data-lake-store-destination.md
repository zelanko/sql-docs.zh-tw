---
title: Azure Data Lake Store 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSDEST.F1
- sql14.dts.designer.afpadlsdest.f1
ms.assetid: 4c4f504f-dd2b-42c5-8a20-1a8ad9a5d632
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d934cafef262f5c07b5eeac95d65abd776d8bb35
ms.sourcegitcommit: fc0eb955b41c9c508a1fe550eb5421c05fbf11b4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/30/2019
ms.locfileid: "66403032"
---
# <a name="azure-data-lake-store-destination"></a>Azure Data Lake Store 目的地

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **Azure Data Lake Store 目的地** 元件可讓 SSIS 套件將資料寫入 Azure Data Lake Store。 支援的檔案格式：文字、Avro 和 ORC。 
  
 **Azure Data Lake Store 目的地**是 [SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。
 
> [!NOTE]
> 為確保 Azure Data Lake Store 連線管理員及使用它的元件 (即 Azure Data Lake Store 來源及 Azure Data Lake Store 目的地) 能夠連接服務，請務必從 [這裡](https://www.microsoft.com/download/details.aspx?id=49492)下載最新版的 Azure Feature Pack。 

## <a name="configure-the-azure-data-lake-store-destination"></a>設定 Azure Data Lake Store 目的地  
1. 將 **Azure Data Lake Store 目的地** 拖放到資料流程設計師，然後在上面按兩下以查看編輯器。  

2.  在 [Azure Data Lake Store 連線管理員]  欄位指定現有的 Azure Data Lake Store 連線管理員，或建立參考 Azure Data Lake Store 服務的新連線管理員。  
  
    1.  在 [檔案路徑]  欄位指定想要寫入資料的檔案名稱。 如果此檔案已經存在，則會覆寫其內容。  
  
    2.  在 [檔案格式]  欄位指定想要使用的檔案格式。  
  
       檔案格式若為文字，則您必須指定 [資料行分隔符號字元]  值。 若檔案中第一個資料列包含資料行名稱，請選取 [第一個資料列的資料行名稱]  。  

       如果檔案格式是 ORC，您會需要為適當的平台安裝 Java Runtime Environment (JRE)。
  
3.  指定連接資訊後，請切換至 [資料行]  頁面，將來源資料行對應至 SSIS 資料流程的目的地資料行。  

## <a name="prerequisite-for-orc-file-format"></a>ORC 檔案格式的必要條件
需要 JAVA 才能使用 ORC 檔案格式。
JAVA 組建架構 (32/64 位元) 應該符合所要使用的 SSIS 執行階段架構。
下列 JAVA 組建已經過測試。

- [Zulu 的 OpenJDK 8u192](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Oracle 的 Java SE Runtime Environment 8u192](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

### <a name="set-up-zulus-openjdk"></a>設定 Zulu 的 OpenJDK
1. 下載並解壓縮安裝 ZIP 套件。
2. 從命令提示字元中，執行 `sysdm.cpl`。
3. 在 [進階]  索引標籤上，選取 [環境變數]  。
4. 在 [系統變數]  區段底下，選取 [新增]  。
5. 針對 [變數名稱]  輸入 `JAVA_HOME`。
6. 選取 [瀏覽目錄]  ，巡覽至解壓縮的資料夾，然後選取 `jre` 子資料夾。
   然後選取 [確定]  ，系統會自動填入 [變數值]  。
7. 選取 [確定]  以關閉 [新增系統變數]  對話方塊。
8. 選取 [確定]  以關閉 [環境變數]  對話方塊。
9. 選取 [確定]  以關閉 [系統內容]  對話方塊。

### <a name="set-up-oracles-java-se-runtime-environment"></a>設定 Oracle 的 Java SE Runtime Environment
1. 下載並執行 exe 安裝程式。
2. 依照安裝程式指示來完成安裝。