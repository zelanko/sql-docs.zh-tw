---
title: 選擇目的地 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 50c9419911f83c98fba5baf0f995ffbeafb916ad
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965648"
---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>選擇目的地 (SQL Server 匯入和匯出精靈)
  使用 [**選擇目的地**] 頁面，即可指定您想要複製之資料的目的地。  
  
 若要深入瞭解此嚮導，請參閱[SQL Server 匯入和匯出嚮導](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要瞭解用來啟動精靈的選項，以及成功執行嚮導所需的許可權，請參閱[執行 SQL Server 匯入和匯出嚮導](start-the-sql-server-import-and-export-wizard.md)。  
  
 「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈」的用途是將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="static-options"></a>靜態選項  
 **目的地**  
 選擇符合目的地資料儲存格式的資料提供者。 您的資料來源可能有一個以上的提供者可用。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client、SQL Server 的 .NET Framework Data Provider，或 SQL Server 的 Microsoft OLE DB 提供者。  
  
> [!NOTE]  
>  若要將資料儲存到 ODBC 目的地，請選取 .NET Framework Data Provider for ODBC。  
  
 [**資料來源**] 屬性的選項數目不定，視電腦上安裝的提供者而定。 下表列出部分常用目的地的選項。 若為其他提供者，請參閱提供者特定文件集。  
  
## <a name="dynamic-options"></a>動態選項  
 下列章節顯示數個資料來源可用的選項。 這裡並未列出 [目的地] 下拉式清單提供的所有目的地。  
  
### <a name="destination--sql-server-native-client-or-microsoft-ole-db-provider-for-sql-server"></a>目的地 = SQL Server Native Client 或 Microsoft OLE DB Provider for SQL Server  
 **伺服器名稱**  
 輸入接收資料的伺服器名稱，或從清單中選擇伺服器。  
  
 **[使用 Windows 驗證]**  
 指定封裝是否使用 Microsoft Windows 驗證來登入資料庫。 建議使用 Windows 驗證，以獲得較佳的安全性。  
  
 **[使用 SQL Server 驗證]**  
 指定封裝是否應使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來登入資料庫。 如果您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，就必須提供使用者名稱和密碼。  
  
 **使用者名稱**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，請指定資料庫連接的使用者名稱。  
  
 **密碼**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，請提供資料庫連接的密碼。  
  
 **Database**  
 從指定之實例上的資料庫清單中選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，或按一下 [**新增**] 來建立新的資料庫。  
  
 **重新整理**  
 按一下 [重新整理]**** 來還原可用資料庫的清單。  
  
 **新增**  
 使用 [**建立資料庫**] 對話方塊來建立新的目的地資料庫。  
  
### <a name="destination--flat-file-destination"></a>目的地 = 一般檔案目的地  
 **檔案名稱**  
 指定儲存資料之檔案的路徑和檔案名稱。 或按一下 [瀏覽]**** 找出檔案。  
  
 **瀏覽**  
 使用 [開啟]**** 對話方塊來找出檔案。  
  
 **Locale**  
 指定用來定義字元排序順序及日期和時間格式的地區設定識別碼 (LCID)。  
  
 **Unicode**  
 指出是否使用 Unicode。 如果使用 Unicode，您就不必指定字碼頁。  
  
 **字碼頁**  
 指定您要使用之語言的字碼頁。  
  
 **[格式]**  
 指出是要使用分隔符號、固定寬度或不齊右的格式。  
  
|值|描述|  
|-----------|-----------------|  
|Delimited (分隔檔)|資料行是以分隔符號分隔，並在 [資料**行**] 頁面上指定。|  
|固定寬度|資料行具有固定寬度。|  
|不齊右|不齊右檔案就是除了最後一個資料行是由資料列分隔符號所分隔之外，其他所有資料行都有固定寬度的檔案。|  
  
 **文字定位項**  
 輸入要使用的文字限定詞。 例如，您可以指定每一個文字資料行都加上引號。  
  
 **第一個資料列的資料行名稱**  
 指出是否在第一個資料列顯示資料行名稱。  
  
### <a name="destination--microsoft-excel"></a>目的地 = Microsoft Excel  
  
> [!NOTE]  
>  只有當您想要連接到使用 Excel 2003 或更早版本的資料來源時，才選取 [ **Microsoft Excel** ]。 若要連接到使用 Excel 2007 的資料來源，請選取 [ **Microsoft Office 12.0 存取資料庫引擎 OLE DB 提供者**]，按一下 [**屬性**]，然後在 [**資料連結屬性**] 對話方塊的 [**全部**] 索引標籤上，針對 [**擴充屬性**] 輸入 `Excel 12.0` 。  
  
 **Excel 檔案路徑**  
 指定用來儲存資料之活頁簿的路徑和檔案名（例如，C:\MyData.xls、 \\\Sales\Database\Northwind.xls）。 或者，按一下 **[流覽]** 以找出活頁簿。  
  
 **瀏覽**  
 使用 [**開啟**] 對話方塊來找出 Excel 活頁簿。  
  
 **Excel 版本**  
 選取目的地活頁簿所使用的 Excel 版本。  
  
> [!NOTE]  
>  當您將資料匯出至 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 目的地時，精靈會使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Excel 目的地元件。 如需有關使用考慮和已知問題的詳細資訊，請參閱[Excel 目的地](../data-flow/excel-destination.md)。  
  
### <a name="destination--microsoft-access"></a>目的地 = Microsoft Access  
  
> [!NOTE]  
>  只有當您想要連接到使用2003或更早版本的資料庫時，才選取 [ **Microsoft Access** ]。 若要連接到使用存取2007的資料庫，請選取 [ **Microsoft Office 12.0 存取資料庫引擎 OLE DB 提供者**]。  
  
 **檔案名稱**  
 指定儲存資料之資料庫檔案的路徑和檔案名（例如，C:\MyData.mdb、 \\ \Sales\Database\Northwind.mdb）。 或者，按一下 **[流覽]** 以找出資料庫檔案。  
  
 **瀏覽**  
 使用 [**開啟**] 對話方塊，流覽至資料庫檔案。  
  
 **使用者名稱**  
 當工作群組資訊檔案與資料庫相關聯時，請指定該資料庫連接的有效使用者名稱。  
  
 **密碼**  
 當工作群組資訊檔案與資料庫相關聯時，請提供該資料庫連接的使用者密碼。 不過，如果資料庫受到所有使用者的單一密碼保護，您就必須在 [**資料連結屬性**] 對話方塊中提供這個值，這可從 [ **Advanced** ] 按鈕存取。  
  
 **進階**  
 使用 [資料連結屬性]**** 對話方塊來指定進階選項，例如資料庫密碼或非預設工作群組資訊檔案。 如需有關 OLE DB 提供者屬性的詳細資訊，請在[MSDN library](https://go.microsoft.com/fwlink/?linkid=62553)的資料存取區段中搜尋。  
  
  
