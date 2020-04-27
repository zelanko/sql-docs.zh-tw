---
title: 變更原始檔控制 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- IDD_SCC_CONNECTION_DIALOG
helpviewer_keywords:
- Change Source Control dialog box
ms.assetid: e6a5d83c-5809-4c56-907a-73d0c7ccdd7a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 939e3befd0cbec87dbba7046761637c4b7655e22
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62812733"
---
# <a name="change-source-control"></a>變更原始檔控制
  建立與管理連接和繫結，連接和繫結會將本機上儲存的方案或專案連結至原始檔控制資料庫資料夾。  
  
## <a name="dialog-box-access"></a>對話方塊存取  
 在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，選取方案總管中的項目。 **在 [檔案**] 功能表上，按一下 [原始檔**控制**]，然後**變更 [原始檔控制**]。  
  
> [!NOTE]  
>  在方案總管中以滑鼠右鍵按一下項目，亦可使用此對話方塊。  
  
## <a name="options"></a>選項。  
 **Bind**  
 建立選取的項目與指定的原始檔控制伺服器位置的關聯。 例如，您可以使用此按鈕，來繫節至最後的已知原始檔控制伺服器和資料庫。 如果找不到最近使用的伺服器資料夾或資料庫，就會提示您指定另一個。  
  
 **瀏覽**  
 導覽至指定之項目的新原始檔控制伺服器位置。  
  
 **資料行**  
 識別要顯示的資料行以及它們顯示的順序。  
  
 **[連接]**  
 在選取的項目和原始檔控制伺服器之間建立連接。  
  
 **聯繫**  
 顯示選取之方案或專案的連接狀態。  
  
 **取消**  
 將電腦上的方案或專案的本機副本與資料庫中的主要副本中斷連接。 在將電腦與原始檔控制伺服器中斷連接之前 (例如，在膝上型電腦上離線工作時)，請使用此命令。  
  
 **確定**  
 接受在對話方塊中所做的變更。  
  
 **提供者**  
 顯示原始檔控制外掛程式的名稱。  
  
 **重新整理**  
 針對此對話方塊中所列出的所有專案，重新整理連接資訊。  
  
 **伺服器繫結**  
 指出項目繫結至原始檔控制伺服器。  
  
 **伺服器名稱**  
 顯示對應之方案或專案所繫結到的原始檔控制伺服器的名稱。  
  
 **方案/專案**  
 顯示目前選取項目中之每個方案和專案的名稱。  
  
 **Sort**  
 排序顯示之資料行的順序。  
  
 **狀態**  
 識別項目的繫結和連接狀態。 可能的值為：  
  
|**選項**|**說明**|  
|----------------|---------------------|  
|有效|項目已正確地繫結並連接到其所屬的伺服器資料夾。|  
|無效|項目不正確地繫結至其所屬的資料夾，或是中斷與其所屬之資料夾的連接。 使用 [**加入至原始檔控制**] 命令，而**不是 [** 系結] 這個專案。|  
|Unknown|尚未決定在原始檔控制下之項目的狀態。|  
|未控制|項目尚未放置在原始檔控制之下。|  
  
 **解除系結**  
 顯示 [**原始檔控制**] 對話方塊，可讓您從原始檔控制中移除選取的專案，並將專案從其目前的資料夾永久解除關聯。  
  
## <a name="see-also"></a>另請參閱  
 [方案總管原始檔控制](../../2014/database-engine/solution-explorer-source-control.md)  
  
  
