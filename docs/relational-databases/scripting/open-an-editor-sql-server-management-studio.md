---
title: 開啟編輯器 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 5d654a60-d205-49d2-a831-b3d986d60024
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26b5683efe327544235913d8e62e100e03ca5a76
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47851056"
---
# <a name="open-an-editor-sql-server-management-studio"></a>開啟編輯器 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  此主題描述如何在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]查詢、MDX、DMX 或 XML/A 編輯器。 開啟時，每個編輯器視窗都會顯示為 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]之中央面板中的索引標籤。  
  
## <a name="before-you-begin"></a>開始之前  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 支援四種編輯器： [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器 (用於編輯 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼)、DMX 及 MDX 編輯器 (以便使用這些語言來編輯指令碼)，以及 XML/A 編輯器 (用於編輯 XML/A 指令碼或 XML 檔案)。 任何編輯器都可以用來編輯文字檔。  
  
### <a name="limitations-and-restrictions"></a>限制事項  
 如果您與使用不同字碼頁之其他網站的使用者共用檔案，您應該利用適當的 Unicode 字碼頁來儲存您的檔案，以防在讀取檔案時發生錯誤。 另外，當儲存 UNIX 或 Macintosh 的檔案時，請務必以適當的文件格式來儲存您的檔案。 請在 **[檔案]** 功能表上，按一下 **[另存新檔]**，從 **[儲存]** 按鈕旁的向下箭頭按一下 **[使用編碼方式儲存]** ，然後在 **[行尾結束符號]** 之下，選擇 **[Unix]** 或 **[Macintosh]**。  
  
### <a name="permissions"></a>[權限]  
 在程式碼編輯器中執行的作業，需要有授與用來登入之驗證帳戶的權限。 例如，如果您使用 [Windows 驗證] 來開啟 [ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器] 視窗，則無法執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，而此陳述式參照您的 Windows 登入帳戶無權存取的物件。  
  
## <a name="how-to-open-editors"></a>如何：開啟編輯器  
 本節說明如何在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中開啟各種編輯器。  
  
### <a name="using-the-filenew-menu"></a>使用檔案/新增功能表  
 在 **[檔案]** 功能表上，按一下 **[新增]**，然後選取其中一個查詢編輯器選項：  
  
-   **使用目前的連接查詢** ：在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中開啟與目前連接相關聯之類型的新編輯器視窗。 此編輯器視窗使用相同的驗證資訊做為目前連接。 例如，如果您在 [物件總管] 中選取 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，然後使用 **[使用目前的連接查詢]**，則 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 會使用相同的驗證資訊開啟與相同執行個體連接的 [ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器]。  
  
-   **Database Engine 查詢** ：開啟新的 [ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器]，和一個對話方塊以取得連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體所需的資訊。  
  
-   **Analysis Services MDX 查詢** ：開啟新的 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] MDX 查詢編輯器]，和一個對話方塊以取得連接至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體所需的資訊。  
  
-   **Analysis Services DMX 查詢** ：開啟新的 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DMX 查詢編輯器]，和一個對話方塊以取得連接至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體所需的資訊。  
  
-   **Analysis Services XML/A 查詢** ：開啟新的 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] XML/A 查詢編輯器]，和一個對話方塊以取得連接至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體所需的資訊。  
  
### <a name="using-the-fileopen-menu"></a>使用檔案/開啟功能表  
 在 **[檔案]** 功能表上，按一下 **[開啟]**，然後導覽至檔案，並開啟該檔案。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 可開啟適用副檔名的編輯器類型、將檔案內容複製到編輯器視窗，也可視需要開啟連接對話方塊。 例如，如果您開啟副檔名為 .sql 的檔案，則 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 會開啟 [ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器] 視窗、複製 .sql 檔案中的內容，並開啟連接對話方塊。 如果您開啟之檔案的副檔名沒有相關聯的特定編輯器，則 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 會開啟文字編輯器視窗，並複製該檔案的內容。  
  
 如需詳細資訊，請參閱 [使副檔名與程式碼編輯器相關聯](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)。  
  
### <a name="using-the-toolbar"></a>使用工具列  
 在 **[標準]** 工具列上，按下列其中一個按鈕：  
  
-   **新增查詢** - 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中開啟與目前連接相關聯之類型的新編輯器視窗。 此編輯器視窗使用相同的驗證資訊做為目前連接。 例如，如果您在 [物件總管] 中選取 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，然後按一下 **[新增查詢]** 按鈕， [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 會使用相同的驗證資訊開啟與相同執行個體連接的 [ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器]。  
  
-   **Database Engine 查詢** ：開啟新的 [ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器]，和一個對話方塊以取得連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體所需的資訊。  
  
-   **Analysis Services MDX 查詢** ：開啟新的 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] MDX 查詢編輯器]，和一個對話方塊以取得連接至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體所需的資訊。  
  
-   **Analysis Services DMX 查詢** ：開啟新的 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DMX 查詢編輯器]，和一個對話方塊以取得連接至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體所需的資訊。  
  
-   **Analysis Services XML/A 查詢** ：開啟新的 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] XML/A 查詢編輯器]，和一個對話方塊以取得連接至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體所需的資訊。  
  
### <a name="using-object-explorer"></a>使用物件總管  
 從 **[物件總管]**：  
  
-   以滑鼠右鍵按一下與 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體連接的伺服器節點，然後選取 [新增查詢]。 這樣會開啟與相同 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體連接的 [[!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器] 視窗，並將此視窗的資料庫內容設定為登入的預設資料庫。  
  
-   以滑鼠右鍵按一下資料庫節點，然後選取 [新增查詢]。 這樣會開啟與相同 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體連接的 [[!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器] 視窗，並將此視窗的資料庫內容設定為相同資料庫。  
  
### <a name="using-solution-explorer"></a>使用方案總管  
 從方案總管中，展開一個資料夾，然後以滑鼠右鍵按一下資料夾內的項目，再按一下 [開啟] 或按兩下項目或檔案。  
  
### <a name="using-template-browser-to-open-the-database-engine-query-editor"></a>使用範本瀏覽器來開啟 Database Engine 查詢編輯器  
  
-   在 **[檢視]** 功能表中，按一下 **[範本總管]**。  
  
-   **[範本瀏覽器]** 視窗即會顯示在右窗格中。  
  
-   按兩下範本，即可開啟含有範本文字的 [Database Engine 查詢] 視窗。 例如，若要開啟 CREATE DATABASE 範本，請開啟 [SQL Server 範本] 資料夾、開啟 [資料庫] 資料夾，然後按兩下 [建立資料庫]。  
  
  
