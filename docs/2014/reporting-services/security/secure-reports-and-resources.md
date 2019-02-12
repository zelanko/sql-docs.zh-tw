---
title: 保護報表和資源的安全 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services], reports
- security [Reporting Services], resources
- reports [Reporting Services], security
- confidential reports [Reporting Services]
- resources [Reporting Services], security
ms.assetid: 63cd55c7-fd2a-49e3-a3f8-59eb1a1c6e83
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a12d538f034f4a3d96726ced32b74f02ec6e73c3
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56023519"
---
# <a name="secure-reports-and-resources"></a>保護報表和資源的安全
  您可以設定個別報表以及資源的安全性，來控制使用者必須對這些項目擁有的存取權程度。 依預設，只有屬於 **管理員** 內建群組成員的使用者才可以執行報表、檢視資源、修改屬性及刪除項目。 其他所有使用者都必須具有針對他們所建立的角色指派，好讓他們存取報表或資源。  
  
## <a name="role-based-access-to-reports-and-resources"></a>以角色為基礎之報表和資源的存取  
 若要授與報表和資源的存取權，您可以讓使用者從父資料夾繼承現有的角色指派，或是在項目本身上建立新的角色指派。  
  
 在大多數情況下，您可能會想要使用從父資料夾繼承而來的權限。 只有在您想要針對不需要知道報表或資源存在的使用者來隱藏報表或資源，或是要提高報表或項目的存取層級時，才應該需要對個別的報表和資源設定安全性。 這些目標不會互斥。 您可以將報表的存取權限制成較小組的使用者，然後提供全部或一部分使用者額外的權限來管理報表。  
  
 您可能需要建立多個角色指派來達成目標。 例如，假設您有一份報表要讓 Ann 與 Fernando 這兩位使用者，以及 Human Resource Managers 群組能夠存取。 Ann 與 Fernando 必須能夠管理報表，但是 Human Resource Managers 成員只需要執行報表。 為了配合所有這些使用者，您要建立三個不同的角色指派：一個讓 Ann 成為報表的內容管理員、一個讓 Fernando 成為報表的內容管理員、一個則支援 Human Resource Managers 群組的僅供檢視工作。  
  
 在報表或資源設定安全性之後，即使將項目移至新位置，這些設定值仍會保留在項目。 例如，若您移動僅少數人擁有存取權的報表，即使將報表移至安全性原則較開放的資料夾，報表仍舊僅供這些使用者使用。  
  
## <a name="mitigating-html-injection-attacks-in-a-published-report-or-document"></a>減少已發行報表或文件中的 HTML 資料隱碼攻擊  
 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，會在執行報表之使用者的安全性識別之下處理報表和資源。 如果報表包含運算式、指令碼、自訂報表項目或自訂組件，則程式碼會在該使用者認證之下執行。 如果資源為包含指令碼的 HTML 文件，則當使用者在報表伺服器上開啟該文件時，將會執行該指令碼。 在報表內執行指令碼或程式碼的能力是某些風險層級所隨附的一項強大功能； 如果程式碼為惡意程式碼，則報表伺服器及執行報表的使用者很容易受到攻擊。  
  
 當您授與以 HTML 形式處理之報表和資源的存取權時，務必要記得報表是在完全信任的模式中處理，而且可能會將潛在的惡意指令碼傳送到用戶端。 根據瀏覽器設定而定，用戶端將會在瀏覽器中指定的信任層級上執行 HTML。  
  
 您可以採取下列預防措施，以減少執行惡意指令碼的風險：  
  
-   當您決定哪些人可以發行內容到報表伺服器時，要有選擇性； 由於存在著發行惡意內容的可能性，所以應該將可以發行內容的使用者限制為少量的受信任使用者。  
  
-   所有發行者都應該避免發行來自未知或未受信任之來源的報表和資源； 必要時，請在文字編輯器中開啟檔案，並尋找可疑的指令碼和 URL。  
  
## <a name="report-parameters-and-script-injection"></a>報表參數和指令碼資料隱碼  
 報表參數會針對整體報表設計和執行提供彈性。 但是，同樣的彈性在某些情況下，可能會遭到攻擊者的引誘攻擊。 若要消除不小心執行惡意指令碼的風險，請只從信任的來源開啟轉譯的報表。 建議您考量潛在 HTML 轉譯器指令碼資料隱碼攻擊的下列情況：  
  
1.  報表包含了具有超連結動作的文字方塊，此動作設定為可能包含惡意文字的參數值。  
  
2.  報表會發行到報表伺服器或者提供給人使用，好讓報表參數值可以從網頁的 URL 加以控制。  
  
3.  攻擊者會建立與網頁或報表伺服器的連結，指定「javascript:\<這裡是惡意指令碼>」形式的參數值，並傳送該連結給引誘攻擊的某個人。  
  
## <a name="mitigating-script-injection-attacks-in-a-hyperlink-in-a-published-report-or-document"></a>減少已發行之報表或文件中的超連結內指令碼資料隱碼攻擊  
 報表可以在報表項目或是部分報表項目的 Action 屬性值中包含內嵌超連結。 當處理報表時，超連結可以繫結至取自外部資料來源的資料。 當惡意使用者修改基礎資料時，超連結可能會遇到指令碼遭人利用的風險。 如果使用者在發行或匯出的報表中按一下連結，惡意指令碼就可能會執行。  
  
 若要消除不小心執行惡意指令碼的風險，包括報表中的連結，只能將超連結繫結至信任來源中的資料。 確認查詢結果中的資料以及將資料繫結至超連結的運算式不會建立可能遭到利用的連結。 例如，請勿讓超連結根據可串連多個資料集欄位資料的運算式。 必要時瀏覽至報表，並使用 [檢視原始檔] 來檢查可疑的指令碼和 URL。  
  
## <a name="mitigating-sql-injection-attacks-in-a-parameterized-report"></a>減少參數化報表中的 SQL 資料隱碼攻擊  
 在任何含有 `String` 類型參數的報表中，請務必使用可用的值清單 (也稱為有效值清單)，並且確認可執行報表的任一使用者只具有檢視報表資料的必要權限。 當您將參數定義為 `String` 類型時，使用者會看到一個可接受任何值的文字方塊。 可用的值清單會限制可輸入的值。 如果報表參數繫結至查詢參數，而且您不要使用可用的值清單，則報表使用者可以在文字方塊中輸入 SQL 語法，如此可能會使您的報表及伺服器暴露在 SQL 資料隱碼攻擊的危險之下。 如果使用者的權限足以執行新的 SQL 陳述式，伺服器可能會出現不良的結果。  
  
 如果報表參數未繫結至查詢參數，且參數值有包含在報表中，則報表使用者就可以在參數值中輸入運算式語法或 URL，並將報表轉譯為 Excel 或 HTML。 如果另一個使用者接著檢視報表並按一下轉譯的參數內容，該使用者可能會不小心執行惡意指令碼或連結。  
  
 若要減輕不小心執行惡意指令碼的風險，請只從信任的來源開啟轉譯的報表。  
  
> [!NOTE]  
>  在舊版的文件集中，有包含將動態查詢建立為運算式的範例； 這種查詢類型會產生 SQL 資料隱碼攻擊的弱點，所以不建議使用。  
  
## <a name="securing-confidential-reports"></a>保護機密報表的安全  
 包含機密資訊的報表應該在資料存取層級受到保護，方法是要求使用者提供存取敏感性資料的認證。 如需詳細資訊，請參閱 [指定報表資料來源的認證及連接資訊](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)。 您也可以保護資料夾的安全，讓未經授權的使用者無法使用它。 如需詳細資訊，請參閱 [保護資料夾的安全](secure-folders.md)。  
  
## <a name="see-also"></a>另請參閱  
 (create-and-manage-role-assignments.md)   
 [設定報表產生器的存取](../report-server/configure-report-builder-access.md)   
 [在原生模式報表伺服器上授與權限](granting-permissions-on-a-native-mode-report-server.md)   
 [保護共用資料來源項目的安全](secure-shared-data-source-items.md)   
 [在 Reporting Services 資料來源中儲存認證](../report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
