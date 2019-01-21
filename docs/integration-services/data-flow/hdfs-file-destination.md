---
title: HDFS 檔案目的地 | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hdfsfiledest.f1
ms.assetid: 4338ce9f-c077-4301-aca5-47ed070ec94d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f18f6b0516ab9ae417251e49f5a3cf24fd2aa997
ms.sourcegitcommit: 1c01af5b02fe185fd60718cc289829426dc86eaa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/10/2019
ms.locfileid: "54185004"
---
# <a name="hdfs-file-destination"></a>HDFS 檔案目的地
  HDFS 檔案目的地元件可讓 SSIS 封裝將資料寫入 HDFS 檔案。 支援的檔案格式為文字、Avro 和 ORC。  
  
 若要設定 HDFS 檔案目的地，請將 HDFS 檔案來源拖放到資料流程設計師，然後按兩下元件以開啟編輯器。  
  
 ![HDFS 檔案目的地編輯器](../../integration-services/data-flow/media/hdfs-file-dest.png "HDFS 檔案目的地編輯器")  
  
## <a name="options"></a>選項。  
 在 [Hadoop File Destination Editor (Hadoop 檔案目的地編輯器)] 對話方塊的 [一般] 索引標籤上，設定下列選項。  
  
|欄位|Description|  
|-----------|-----------------|  
|**Hadoop 連接**|指定現有的 Hadoop 連接管理員或建立新的連接管理員。 此連接管理員會指出 HDFS 檔案的裝載位置。|  
|**檔案路徑**|指定 HDFS 檔案的名稱。|  
|**檔案格式**|指定 HDFS 檔案的格式。 可用的選項為文字、Avro 和 ORC。|  
|**資料行分隔符號字元**|如果您選取文字格式，請指定資料行分隔符號字元。|  
|**第一個資料列的資料行名稱**|如果您選取文字格式，請指定檔案中的第一個資料列是否包含資料行名稱。|  
  
 設定這些選項之後，請選取 [資料行] 索引標籤，將資料流程中的來源資料行對應至目的地資料行。  

::: moniker range=">= sql-server-ver15"
## <a name="prerequisite-for-orc-format"></a>ORC 格式的先決條件

您必須先安裝適用於適當平台的 1.7.51 版或更新版本的 Java Runtime Environment (JRE)，才能使用 OCR 檔案格式。

同時支援 Zulu 和 Oracle JRE。
-   [Zulu JRE](https://www.azul.com/downloads/zulu/zulu-windows/)
-   [Oracle JRE](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)

### <a name="set-up-the-zulu-jre"></a>安裝 Zulu JRE

1. 下載 Zulu OpenJDK 安裝 zip 套件並解壓縮。

2.  從命令提示字元中，執行 `sysdm.cpl`。

3. 在 [進階] 索引標籤上，選取 [環境變數]。

4. 在 [系統變數] 區段底下，選取 [新增]。

5. 針對 [變數名稱] 輸入 `JAVA_HOME`。

6. 選取 [瀏覽目錄]，瀏覽至 Zulu OpenJDK 安裝資料夾，然後選取 `jre` 子資料夾。 然後選取 [確定]。 系統會自動填入變數值。

7. 選取 [確定] 以關閉 [新增系統變數] 對話方塊。

8. 選取 [確定] 以關閉 [環境變數] 對話方塊。

### <a name="set-up-the-oracle-jre"></a>安裝 Oracle JRE

1. 下載並執行 Oracle JRE exe 安裝程式。

1. 依照安裝程式指示來完成安裝。

::: moniker-end

## <a name="see-also"></a>另請參閱  
 [Hadoop 連接管理員](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [HDFS 檔案來源](../../integration-services/data-flow/hdfs-file-source.md)  
