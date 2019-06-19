---
title: 彈性檔案目的地 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpextfiledest.f1
- sql14.dts.designer.afpextfiledest.f1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2a0ffa4b881fe550aba6c547fcea690932eef110
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66462620"
---
# <a name="flexible-file-destination"></a>彈性檔案目的地

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

**彈性檔案目的地**元件可讓 SSIS 套件將資料寫入至各種支援的儲存體服務。

以下為目前支援的儲存體服務：

- [Azure Blob 儲存體](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction) \(部分機器翻譯\)
   
將 [彈性檔案目的地] 拖放到資料流程設計師，然後按兩下以查看編輯器。
  
**彈性檔案目的地**是 [SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。  

**彈性檔案目的地編輯器**提供下列屬性。

- **檔案連線管理員類型：** 指定來源連線管理員類型。 然後選擇一個現有的指定類型，或建立新的。
- **資料夾路徑：** 指定目的地資料夾路徑。
- **檔案名稱：** 指定目的地檔案名稱。
- **檔案格式：** 指定目的地檔案格式。 支援的格式為 **Text**、**Avro**、**ORC**、**Parquet**。
- **資料行分隔符號字元：** 指定要用來作為資料行分隔符號的字元 (不支援多字元分隔符號)。
- **第一個資料列作為資料行名稱：** 指定是否要將資料行名稱寫入至第一個資料列。
- **壓縮檔案：** 指定是否要壓縮檔案。
- **壓縮類型：** 指定要使用的壓縮格式。 支援的格式為 **GZIP**、**DEFLATE**、**BZIP2**。
- **壓縮層級：** 指定要使用的壓縮層級。

**進階編輯器**提供下列屬性。

- **rowDelimiter：** 用來分隔檔案中資料列的字元。 只允許一個字元。 **預設**值為 \r\n。
- **escapeChar：** 用來逸出輸入檔內容中資料行分隔符號的特殊字元。 您無法為資料表同時指定 escapeChar 和 quoteChar。 只允許一個字元。 無預設值。
- **quoteChar：** 用來為字串值加上引號的字元。 系統會將引號字元內資料行和資料列分隔符號視為字串值的一部分。 這個屬性同時適用於輸入和輸出資料集。 您無法為資料表同時指定 escapeChar 和 quoteChar。 只允許一個字元。 無預設值。
- **nullValue：** 用來代表 Null 值的一或多個字元。 **預設**值是 \N。
- **encodingName：** 指定編碼名稱。 請參閱 [Encoding.EncodingName](https://docs.microsoft.com/en-us/dotnet/api/system.text.encoding?redirectedfrom=MSDN&view=netframework-4.8) 屬性。
- **skipLineCount：** 表示從輸入檔讀取資料時會略過非空白資料列的數目。 如果同時指定 skipLineCount 和 firstRowAsHeader，則會先略過行，然後從輸入檔讀取標頭資訊。
- **treatEmptyAsNull：** 指定從輸入檔讀取資料時是否將 Null 或空字串視為 Null 值。 **預設**值為 True。

指定連接資訊後，請切換至 [資料行]  頁面，將來源資料行對應至 SSIS 資料流程的目的地資料行。

**ORC/Parquet 檔案格式的必要條件**

需要 Java 才能使用 ORC/Parquet 檔案格式。
JAVA 組建架構 (32/64 位元) 應該符合所要使用的 SSIS 執行階段架構。
下列 JAVA 組建已經過測試。

- [Zulu 的 OpenJDK 8u192](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Oracle 的 Java SE Runtime Environment 8u192](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

**設定 Zulu 的 OpenJDK**

1. 下載並解壓縮安裝 ZIP 套件。
2. 從命令提示字元中，執行 `sysdm.cpl`。
3. 在 [進階] 索引標籤上，選取 [環境變數]。
4. 在 [系統變數] 區段底下，選取 [新增]。
5. 針對 [變數名稱] 輸入 `JAVA_HOME`。
6. 選取 [瀏覽目錄]，巡覽至解壓縮的資料夾，然後選取 `jre` 子資料夾。
   然後選取 [確定]，系統會自動填入 [變數值]。
7. 選取 [確定] 以關閉 [新增系統變數] 對話方塊。
8. 選取 [確定] 以關閉 [環境變數] 對話方塊。
9. 選取 [確定] 以關閉 [系統內容] 對話方塊。

**設定 Oracle 的 Java SE Runtime Environment**

1. 下載並執行 exe 安裝程式。
2. 依照安裝程式指示來完成安裝。
