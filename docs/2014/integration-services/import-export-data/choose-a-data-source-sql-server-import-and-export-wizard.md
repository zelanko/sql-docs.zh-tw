---
title: 選擇資料來源 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b6e399cf6c145f36febd9b32ae7a84c54741bb43
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381208"
---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>選擇資料來源 (SQL Server 匯入和匯出精靈)
  使用**選擇資料來源**頁面，即可指定您想要複製的資料來源。  
  
 若要深入了解此精靈，請參閱[SQL Server 匯入和匯出精靈](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要深入了解啟動精靈，選項和相關的權限，才能成功執行精靈，請參閱[執行 SQL Server 匯入和匯出精靈](start-the-sql-server-import-and-export-wizard.md)。  
  
 「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈」的用途是將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>選項。  
 **資料來源**  
 選擇符合來源之資料儲存格式的資料提供者。 您的資料來源可能有一個以上的提供者可用。 例如，使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client、.NET Framework Data Provider for SQL Server 或 Microsoft OLE DB Provider for SQL Server。  
  
 **資料來源**屬性有不同數目的選項，而這取決於電腦上安裝的提供者。 下表列出一些經常使用之目的地的選項。 若為其他提供者，請參閱提供者特定文件集。  
  
## <a name="dynamic-options"></a>動態選項  
 下列章節顯示數個資料來源可用的選項。 此處並未列出 [資料來源] 下拉式清單中所有可用的資料來源。  
  
### <a name="data-source--sql-server-native-client-and-microsoft-ole-db-provider-for-sql-server"></a>資料來源 = SQL Server Native Client 和 Microsoft OLE DB Provider for SQL Server  
 **伺服器名稱**  
 輸入包含資料之伺服器的名稱，或者從清單中選擇伺服器。  
  
 **[使用 Windows 驗證]**  
 指定封裝是否應使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 驗證來登入資料庫。 建議使用 Windows 驗證，以獲得較佳的安全性。  
  
 **[使用 SQL Server 驗證]**  
 指定封裝是否應使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來登入資料庫。 如果您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，就必須提供使用者名稱和密碼。  
  
 **使用者名稱**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，請指定資料庫連接的使用者名稱。  
  
 **密碼**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，請提供資料庫連接的密碼。  
  
 **[資料庫備份]**  
 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之指定執行個體上的資料庫清單中選取。  
  
 **[重新整理]**  
 按一下 [重新整理] 來還原可用資料庫的清單。  
  
### <a name="data-source--net-framework-data-provider-for-sql-server"></a>資料來源 = .NET Framework Data Provider for SQL Server  
 此頁面會依字母順序呈現 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的選項清單。 最重要的選項列於下表中。  
  
 **資料來源**  
 輸入包含資料之伺服器的名稱，或者從清單中選擇伺服器。  
  
 **初始目錄**  
 輸入來源資料庫的名稱。  
  
 **整合式安全性**  
 指定 `True` 以使用 Windows 整合式驗證進行連接 (建議使用)，或指定 `False` 以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接。 如果您指定 `False`，則必須輸入使用者識別碼和密碼。 預設值是 `False`。  
  
 **使用者識別碼**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，請指定資料庫連接的使用者名稱。  
  
 **密碼**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，請提供資料庫連接的密碼。  
  
 選取此提供者時所列出的其他選項並非必要的，即可成功連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來源資料庫。 如需其他選項的描述，請參閱 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Software Development Kit 中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Provider for [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的文件集。  
  
### <a name="data-source--microsoft-excel"></a>資料來源 = Microsoft Excel  
  
> [!NOTE]  
>  選取  **Microsoft Excel**只有當您想要連接到資料來源使用 Excel 2003 或更早版本。 若要連接至使用 Excel 2007 資料來源，請選取**Microsoft Office 12.0 Access 資料庫引擎 OLE DB 提供者**，按一下**屬性**，然後在**所有** 索引標籤**資料連結屬性**對話方塊方塊中，輸入`Excel 12.0`做為值**擴充屬性**。  
  
 **Excel 檔案路徑**  
 指定要從中匯入資料之試算表的路徑和檔案名稱。 例如， **C:\MyData.xls， \\\Sales\Database\Northwind.xls**。 或按一下 [瀏覽]。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出試算表。  
  
 **Excel 版本**  
 選取儲存來源資料之 Excel 的版本。  
  
> [!NOTE]  
>  當您從 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 來源匯入資料時，精靈會使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Excel 來源元件。 如需使用方式考量與已知問題的資訊，請參閱 [Excel 來源](../data-flow/excel-source.md)。  
  
### <a name="data-source--microsoft-access"></a>資料來源 = Microsoft Access  
  
> [!NOTE]  
>  選取  **Microsoft Access**只有當您想要連接至使用 Access 2003 資料庫或更早版本。 若要連線至使用 Access 2007 資料庫，選取**Microsoft Office 12.0 Access 資料庫引擎 OLE DB 提供者**改。  
  
 **檔案名稱**  
 指定要從中匯入資料之資料庫檔案的路徑和檔案名稱。 例如 **C:\MyData.mdb, \\\Sales\Database\Northwind.mdb**。 或按一下 [瀏覽]。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出資料庫檔案。  
  
 **使用者名稱**  
 當工作群組資訊檔案與資料庫相關聯時，請指定該資料庫連接的有效使用者名稱。  
  
 **密碼**  
 當工作群組資訊檔案與資料庫相關聯時，請提供該資料庫連接的使用者密碼。 不過，如果所有使用者的單一密碼保護資料庫，您必須提供此值**資料連結屬性**對話方塊，即可存取**進階**。  
  
 **進階**  
 您可能想要指定進階的選項，例如資料庫密碼或非預設的工作群組資訊檔案中，使用**資料連結屬性** 對話方塊。 如需有關 OLE DB 提供者屬性的詳細資訊，請搜尋中的 [資料存取] 區段[MSDN library](https://go.microsoft.com/fwlink/?linkid=62553)。  
  
### <a name="data-source--flat-file-source"></a>資料來源 = 一般檔案來源  
 如需有關一般檔案資料來源之選項的資訊，請參閱下列主題。  
  
 [一般檔案連線管理員編輯器 &#40;[一般]頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
 [一般檔案連線管理員編輯器 &#40;[資料行] 頁面&#41;](../flat-file-connection-manager-editor-columns-page.md)  
  
 [一般檔案連線管理員編輯器 &#40;[進階] 頁面&#41;](../flat-file-connection-manager-editor-advanced-page.md)  
  
 [一般檔案連接管理員編輯器 &#40;[預覽] 頁面&#41;](../flat-file-connection-manager-editor-preview-page.md)  
  
  
