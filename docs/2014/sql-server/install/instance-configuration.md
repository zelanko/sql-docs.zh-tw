---
title: 執行個體組態 |Microsoft Docs
ms.custom: ''
ms.date: 2016-05-04
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9177aa0abe0a5f2a3746486c5cf71163bcd1e1be
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52791296"
---
# <a name="instance-configuration"></a>執行個體組態
  請使用 **安裝精靈的** [執行個體組態] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 頁面，指定要建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的預設執行個體還是具名執行個體。 如果尚未安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，則除非您指定具名執行個體，否則將會建立預設執行個體。  
  
 每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體都包含一組不同的服務，而這些服務對於定序和其他選項具有特定設定。 目錄結構、登錄結構和服務名稱都反映出在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間建立的執行個體名稱和特定的執行個體識別碼。  
  
 執行個體是預設執行個體或具名執行個體。 預設執行個體名稱是 MSSQLSERVER。 它不需要用戶端指定執行個體名稱來進行連接。 具名執行個體由使用者在安裝期間決定。 您可以將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝為具名執行個體，而不需要先安裝預設執行個體。 一次只有一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝 (不論版本為何) 可以是預設執行個體。  
  
 **警示 ！** 透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep，當您完成備妥的執行個體時，就可以在 [執行個體組態] 頁面上指定執行個體名稱。 如果電腦上沒有任何現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設執行個體，您就可以選擇將所完成的備妥執行個體設定為預設執行個體。  
  
## <a name="multiple-instances"></a>多個執行個體  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援單一伺服器或處理器上的多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，但是只有一個執行個體可以是預設執行個體； 其他所有的執行個體都必須是具名執行個體。 電腦可同時執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的多個執行個體，每一個執行個體的執行與其他執行個體無關。  
  
 如需詳細資訊，請參閱 [Maximum Capacity Specifications for SQL Server](../maximum-capacity-specifications-for-sql-server.md)。  
  
## <a name="options"></a>選項。  
 僅限容錯移轉叢集執行個體 - 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集網路名稱。 這個名稱會在網路上識別容錯移轉叢集執行個體。  
  
 預設或具名執行個體 - 在決定要安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設執行個體還是具名執行個體時，請考量以下資訊：  
  
-   如果您計劃在資料庫伺服器上安裝單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，它應該是預設執行個體。  
  
-   當您打算在相同電腦上擁有多個執行個體時，請使用具名執行個體。 一個伺服器只能主控一個預設執行個體。  
  
-   安裝 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 的任何應用程式都應該將它安裝為具名執行個體。 這種作法可以減少將多個應用程式安裝在相同電腦時所造成的衝突。  
  
 **預設執行個體**  
 選取這個選項可安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設執行個體。 電腦只能主控一個預設執行個體；所有其他執行個體都必須加以命名。 不過，如果您已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設執行個體，您可將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的預設執行個體加入相同電腦中。  
  
 **具名執行個體**  
 選取這個選項可建立新的具名執行個體。 當您為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體命名時，請注意以下事項：  
  
-   執行個體名稱不區分大小寫。  
  
-   執行個體名稱不能以底線 (_) 開始或結束。  
  
-   執行個體名稱不得包含 "Default" 一詞或其他保留關鍵字。 如果在執行個體名稱中使用了保留關鍵字，會發生安裝程式錯誤。 如需詳細資訊，請參閱[保留關鍵字 &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reserved-keywords-transact-sql)。  
  
-   如果您為執行個體名稱指定 MSSQLServer，將會建立預設執行個體。  
  
-   安裝 [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] 時，一律會安裝成 'PowerPivot' 的具名執行個體。 您無法針對這個功能角色指定不同的執行個體名稱。  
  
-   執行個體名稱限制為 16 個字元。  
  
-   執行個體名稱中的第一個字元必須是字母。 可接受的字母是由 Unicode Standard 2.0 所定義的字母。 這些包括拉丁字元 a-z、A-Z 及其他語言的字母字元。  
  
-   後續字元可以是 Unicode 標準 2.0 定義的字母、基本拉丁文或其他國家 (地區) 指令碼中的十進位數字、錢幣符號($) 或底線 (_)。  
  
-   執行個體名稱中不允許內嵌空格或其他特殊字元。 此外，也不允許反斜線 (\\)、逗號 (,)、冒號 (:)、分號 (;)、單引號 (')、＆ 符號 (&)、連字號 (-) 和 At 符號 (@)。  
  
-   **只有在目前的 Windows 字碼頁中有效的字元可以用於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體名稱。如果使用不支援的 Unicode 字元時，會發生安裝錯誤。**  
  
 **偵測到的執行個體和功能**  
 在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式的電腦上檢視已安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體和元件的清單。  
  
 **執行個體識別碼** ：依預設，此執行個體名稱會當作執行個體識別碼使用。 這是用來識別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的安裝目錄和登錄機碼。 這是預設執行個體和具名執行個體的狀況。 如果是預設執行個體，執行個體名稱和執行個體識別碼將會是 MSSQLSERVER。 若要使用非預設的執行個體識別碼，請在 **[執行個體識別碼]** 欄位中指定它。  
  
> [!IMPORTANT]  
>  透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep，顯示在這個頁面上的執行個體識別碼就是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep 程序之準備映像步驟期間所指定的執行個體識別碼。 您無法在完成映像步驟期間指定不同的執行個體識別碼。  
  
> [!NOTE]  
>  不支援以底線 (_) 為開頭或是包含數字符號 (#) 或貨幣符號 ($) 的執行個體識別碼。  
  
 如需目錄、檔案位置和執行個體識別碼命名的詳細資訊，請參閱 [SQL Server 的預設和具名執行個體的檔案位置](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)。  
  
 給定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的所有元件都會當做一個單位來管理。 所有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack 和升級項目都會套用至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的每一個元件。  
  
 所有共用相同執行個體名稱之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有元件，都必須符合下列準則：  
  
-   **相同的版本**  
  
-   **相同的版本**  
  
-   **相同語言設定**  
  
-   **相同叢集狀態**  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 無法識別叢集。  
  
-   **相同作業系統**  
  
  
