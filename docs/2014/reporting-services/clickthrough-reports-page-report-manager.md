---
title: 點選連結報表頁面（報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.drilthroughreports.f1
ms.assetid: e96cdeba-452b-45a8-9bcf-b75d76261e31
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d996463baaed3095b6866fa2da88ed811745878d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109800"
---
# <a name="clickthrough-reports-page-report-manager"></a>點選連結報表頁面 (報表管理員)
  當您按一下報表中包含的互動式資料時，點選連結報表就會顯示相關資料的資料表。 這些報表是報表伺服器根據您用來建立報表之模型中包含的資訊所產生的。 如果您不想要使用報表伺服器所產生的點選連結報表，可以建立自訂報表，以便將它們發行至報表伺服器並對應至模型中定義的互動式資料點。 您必須根據相同的模型在報表產生器中建立這些自訂報表，然後將它們發行至報表伺服器。 若要將自訂報表對應至模型中的項目，請使用報表管理員中的 [點選連結報表] 頁面。  
  
 [點選連結報表] 頁面會提供將預先定義且已發行之報表產生器報表對應至模型內特定實體、資料夾和項目的方式。 當您將報表對應至模型內的項目時，導覽到該項目的使用者會取得自訂報表，而非報表伺服器所產生的暫存報表。  
  
 如果您提供的是自訂報表，就應同時包含單一執行個體和多重執行個體版本的報表。 使用者導覽到特定實體的資料路徑，會決定在執行階段是要向使用者顯示單一執行個體或多重執行個體報表。 您總是無法事先知道，是否不需要報表的某個特定版本。  
  
 您對應至實體的自訂報表，會透過報表伺服器資料夾階層加以保護。 如果您將模型項目對應至報表，而且已導覽到它的使用者無法使用該報表，則使用者就會取得由報表伺服器所產生的暫存報表，而非您預期的自訂報表。  
  
 雖然您可以選取任何能夠存取的報表，請只選取特別針對您正在設定之模型所建立的報表。  
  
> [!NOTE]  
>  並非 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的所有版本都可使用點選連結報表。 如需版本支援的功能清單[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請參閱[SQL Server 2014 版本支援的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。 如果您不確定您組織執行的是哪個版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，請連絡資料庫管理員。  
  
## <a name="navigation"></a>導覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
###### <a name="to-open-the-clickthrough-reports-page"></a>若要開啟點選連結報表頁面  
  
1.  開啟報表管理員，然後找出您想要將點選連結報表對應至模型中之實體的模型。  
  
2.  將滑鼠停留在該模型上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]** 。 這樣就會開啟該模型的 **[一般]** 屬性頁面。  
  
4.  選取 **[點選連結]** 索引標籤。  
  
## <a name="options"></a>選項。  
 **模型項目階層**  
 顯示模型命名空間中，您可以為其提供自訂報表的實體、資料夾和項目。  
  
 **單一執行個體報表**  
 指定當使用者導覽需要單一執行個體資料的檢視時，要使用的自訂報表。 按一下瀏覽按鈕，即可選取您要使用的報表。  
  
 **多個執行個體報表**  
 指定當使用者導覽需要多重執行個體資料的檢視時，要使用的自訂報表。 按一下瀏覽按鈕，即可選取您要使用的報表。  
  
## <a name="see-also"></a>另請參閱  
 [發行報表](../../2014/reporting-services/publish-reports.md)  
  
  
