---
title: "已發行的報表-SharePoint 整合模式上設定參數 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint integration [Reporting Services], content management
- report parameters [Reporting Services]
ms.assetid: dec5d985-a6c1-4dd8-8a66-a848e89a2e18
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ba05b4727499c702b9f8827de9564aad444c1ebc
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="set-parameters-on-a-published-report---sharepoint-integrated-mode"></a>設定已發行的報表-SharePoint 整合模式上的參數
  參數化報表是指可接受輸入值的報表，而這些輸入值會在您執行報表時用來篩選資料。 參數是在報表建立時定義的。 根據報表參數在報表定義中的定義方式，它可能會接受單一值、多個值或動態值，而這些值會變更以便回應之前的選取項目 (例如，當您選取產品類別目錄時，下一個選取項目可能是來自該類別目錄的特定產品)。 參數可能會有預設值，而且此值可用來自動執行已篩選的報表版本或可能由不同的值取代。  
  
 這些屬性可以在報表定義中設定，或是在已經發行報表後設定。 雖然您可以在已發行的報表中修改某些參數屬性來變更值並顯示屬性，但是您無法變更參數名稱或資料類型。 參數名稱與資料類型僅能透過報表定義中的報表作者變更。  
  
 若要執行參數化的報表，雖然報表可能包含要從中選擇之有效值的下拉式清單，但是您通常必須知道要輸入哪些值。  
  
 若要在已發行的報表上設定參數屬性，您必須擁有該報表的「編輯項目」權限。 您可以在從 SharePoint 網站執行的報表上，修改部分或所有參數屬性。 但是，您無法透過儲存想要重複使用之參數值的組合，個人化報表。 您所指定的任何預設值都會由開啟報表的所有使用者使用。  
  
 如果報表內嵌在設定為永遠顯示該報表的報表檢視器 Web 組件中，在報表檢視器 Web 組件上設定屬性。 如需詳細資訊，請參閱[將報表檢視器 Web 組件加入至網頁 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)。  
  
### <a name="to-run-a-parameterized-report"></a>執行參數化的報表  
  
1.  開啟包含報表的文件庫。  
  
2.  按一下報表名稱。 您必須事先知道哪些報表具有參數。 報表上沒有視覺上的識別碼可以表示該報表已被參數化。  
  
3.  當報表開啟時，指定您要使用的參數。 根據屬性在報表檢視器 Web 組件上的設定，可能可以顯示、折疊或隱藏 [參數] 區域。  
  
    1.  如果有顯示 [參數] 區域，為每個參數選擇一個值。  
  
    2.  如果有一條細色帶沿著中央有個箭號的報表長度向下，表示 [參數] 區域是折疊的。 您可以按一下箭號，來展開它。  
  
    3.  如果 [參數] 區域已隱藏，您就無法指定值。  
  
4.  在 [參數] 區域底部按一下 [套用] 以執行報表。  
  
     有時候，指定了值的組合可能也無法提供您所預期的結果。 如果您沒有取得所需的資訊，可能就需要由報表作者修改報表。  
  
5.  按一下 **[確定]**。  
  
### <a name="to-set-parameter-properties"></a>設定參數屬性  
  
1.  開啟包含報表的文件庫或資料夾。  
  
2.  指向報表，然後按一下向下箭號。  
  
3.  按一下 [管理參數]。 如果報表包含參數，每個參數都會列在頁面上。 此清單會顯示參數名稱、資料類型、預設使用的資料值，以及開啟報表時它是否會顯示在參數區域中。  
  
4.  按一下清單中的參數，即可修改其設定。  
  
5.  在 [預設值] 中，輸入參數的值。 由於此值將不會進行驗證，因此請確定您提供了適用於報表的值。  
  
    1.  如果您要使用建立報表時所定義的預設值，選擇 [使用報表定義中指定的值運算式]。 如果報表定義不提供預設值，將無法使用此選項。  
  
    2.  如果您要為報表定義預設值指定一個取代值，選擇 [覆寫報表預設值]。 對於接受 Null 值的報表參數，您可以根據該參數，選擇性地選取 [Null] 核取方塊以防止篩選。  
  
    3.  如果您想讓每位使用者指定值，然後再處理報表，請選擇 [Parameter does not have a default value (參數沒有預設值)]。 如果您選取這個選項，就應該設定提示使用者指定值的顯示設定。  
  
     請注意，如果所有參數值都具有預設值，當使用者開啟報表時，報表將會使用這些值自動執行。 不過，如果有顯示參數區域，使用者可以覆寫預設值，然後重新執行報表。  
  
6.  您可以設定顯示選項，以便決定參數是否會顯示。  
  
    1.  選擇 [提示]，即可在頁面上顯示參數。 您可以指定出現在欄位中的提示文字，以提供關於使用者必須提供之資料格式或類型的簡短說明。  
  
    2.  如果您要使用預設值，而且不想讓此參數顯示在 [參數] 區域中，請選擇 [隱藏]。  
  
    3.  如果您要使用預設值，而且不想讓此參數顯示在 [參數] 區域或訂閱頁面上，請選擇 [內部]。  
  
7.  按一下 **[套用]**。  
  
## <a name="see-also"></a>請參閱＜  
 [報表伺服器項目的 SharePoint 網站和清單權限參考](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)  
  
  
