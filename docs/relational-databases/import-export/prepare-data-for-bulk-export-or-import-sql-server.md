---
title: 準備大量匯出或匯入的資料 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], planning
- bulk importing [SQL Server], from a CSV file
- data formats [SQL Server], planning operations
- CSV files [SQL Server]
- quoted fields in CSV files [SQL Server]
ms.assetid: 783fd581-2e5f-496b-b79c-d4de1e09ea30
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3489ef2c55de4ce332f53bccc167f2ff052f19d9
ms.sourcegitcommit: 04c031f7411aa33e2174be11dfced7feca8fbcda
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/30/2019
ms.locfileid: "64946155"
---
# <a name="prepare-data-for-bulk-export-or-import-sql-server"></a>準備大量匯出或匯入的資料 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本節討論關於大量匯出作業之規劃與大量匯入作業之需求的考量。  
  
> [!NOTE]  
>  如果您不確定如何格式化資料檔以進行大量匯入，請使用 **bcp** 公用程式將資料從資料表匯出至資料檔。 此檔案中每個資料欄位的格式會顯示將資料大量匯入對應資料表資料行所需的格式。 請使用資料檔案欄位的相同資料格式。  
  
## <a name="data-file-format-considerations-for-bulk-export"></a>大量匯出的資料檔格式考量  
 使用 **bcp** 命令執行大量匯出作業之前，請考慮下列事項：  
  
-   將資料匯出至檔案時， **bcp** 命令會使用指定的檔案名稱自動建立資料檔。 如果該檔名已在使用中，則大量複製到資料檔的資料會覆寫檔案現有的內容。  
  
-   從資料表或檢視大量匯出到資料檔，需要大量複製的資料表或檢視之 SELECT 權限。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可使用平行掃描來擷取資料。 因此，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體大量匯出的資料表資料列，通常不能保證在資料檔中具有特定順序。 若要讓大量匯出的資料表資料列以特定順序顯示在資料檔中，請使用 **queryout** 選項從查詢進行大量匯出，以及指定 ORDER BY 子句。  
  
## <a name="data-file-format-requirements-for-bulk-import"></a>大量匯入的資料檔格式需求  
 若要從資料檔匯入資料，該檔案必須符合下列基本需求：  
  
-   資料必須為資料列與資料行的格式。  
  
> [!NOTE]  
>  因為在大量匯入處理期間可略過或重新排列資料行，資料檔的結構並不需要與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表的結構相同。  
  
-   資料檔中的資料必須為支援的格式，如字元或原生格式。  
  
-   資料的格式可以是字元或原生二進位格式，包括 Unicode。  
  
-   若要使用 **bcp** 命令、BULK INSERT 陳述式或 INSERT ...SELECT * FROM OPENROWSET(BULK...) 陳述式來匯入資料，目的地資料表必須已經存在。  
  
-   資料檔中的每個欄位都必須與目標資料表中的對應資料行相容。 例如，無法將 **int** 欄位載入 **datetime** 資料行。 如需詳細資訊，請參閱[大量匯入或大量匯出的資料格式 &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md) 和[使用 bcp 指定相容性的資料格式 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)。  
  
    > [!NOTE]  
    >  若要指定從資料檔而非整個檔案中匯入資料列子集，您可以搭配使用 **bcp** 命令與 **-F** *first_row* 參數及/或 **-L** *last_row* 參數。 如需相關資訊，請參閱 [bcp Utility](../../tools/bcp-utility.md)。  
  
-   若要從包含固定長度或固定寬度欄位的資料檔案匯入資料，請使用格式檔案。 如需詳細資訊，請參閱 [XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 大量匯入作業不支援逗號分隔值 (CSV) 檔案。 不過，在某些情況下，CSV 檔案可用來當做資料檔案，以便將資料大量匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請注意，CSV 檔案的欄位結束字元不必是逗號。 為了能夠當做資料檔使用來進行大量匯入，CSV 檔案必須符合下列限制：  
  
    -   資料欄位永遠不會包含欄位結束字元。  
  
    -   引號 ("") 中會括住資料欄位內的所有值或是不括住任何值。  
  
     若要從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] FoxPro 或 Visual FoxPro 資料表 (.dbf) 檔案或 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 工作表 (.xls) 檔案大量匯入資料，您必須將該資料轉換成符合前述限制的 CSV 檔案。 副檔名通常為 .csv。 然後，您就可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 大量匯入作業中，將此 .csv 檔案當做資料檔使用。  
  
     在 32 位元系統上，您可以搭配 OLE DB Provider for Jet 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OPENROWSET [，將 CSV 資料匯入](../../t-sql/functions/openrowset-transact-sql.md) 資料表，而不需要將大量匯入最佳化。 Jet 會將文字檔視為資料表，其中包含與資料來源位於相同目錄中之 schema.ini 檔所定義的結構描述。  若是 CSV 資料，schema.ini 檔中的其中一個參數將會是 "FORMAT=CSVDelimited"。 若要使用此解決方案，您需要了解 Jet Test IISAMm 如何運作 (其連接字串語法、schema.ini 用法、登錄設定選項等等)。  此資訊的最佳來源為 Microsoft Access 說明以及知識庫 (KB) 文件。 如需詳細資訊，請參閱[初始化文字資料來源驅動程式](https://msdn.microsoft.com/library/office/ff834391.aspx)、[如何搭配安全保護 Access 資料庫的連結伺服器使用 SQL Server 7.0 分散式查詢](https://go.microsoft.com/fwlink/?LinkId=128504)、[如何：使用 Jet OLE DB Provider 4.0 連線到 ISAM 資料庫 ](https://go.microsoft.com/fwlink/?LinkId=128505)，以及[如何使用 Jet 提供者的文字 IIsam 開啟分隔的文字檔](https://go.microsoft.com/fwlink/?LinkId=128501)。  
  
 此外，將資料從資料檔大量匯入到資料表中需要下列：  
  
-   使用者必須具有該資料表的 INSERT 與 SELECT 權限。 使用者在使用需要資料定義語言 (DDL) 作業的選項 (如停用條件約束) 時，也需要 ALTER TABLE 權限。  
  
-   當您使用 BULK INSERT 或 INSERT ...SELECT * FROM OPENROWSET(BULK...) 來大量匯入資料時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序的安全性設定檔 (若使用者利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供的登入來登入) 和用於委託安全性的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入，必須可存取資料檔以進行讀取作業。 此外，使用者必須具有 ADMINISTER BULK OPERATIONS 權限才能讀取檔案。  
  
> [!NOTE]  
>  系統並不支援大量匯入到資料分割檢視，而嘗試將資料大量匯入到資料分割檢視會失敗。  
  
## <a name="external-resources"></a>外部資源  
 [如何將 Excel 中的資料匯入到 SQL Server](https://support.microsoft.com/kb/321686)  
  
## <a name="change-history"></a>變更記錄  
  
|更新的內容|  
|---------------------|  
|已加入使用 OLE DB Provider for Jet 匯入 CSV 資料的相關資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)   
 [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
  
