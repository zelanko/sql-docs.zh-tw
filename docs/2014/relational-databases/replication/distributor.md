---
title: 散發者 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.replicationutilities.selectdistributor.f1
ms.assetid: 787f0e9c-09dd-438a-bc04-5b8f99c127b8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6c0a98aa13b4453244c8ed565a950660a20e5a3c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721305"
---
# <a name="distributor"></a>散發者
  **[散發者]** 頁面會出現在設定散發精靈和新增發行集精靈中。 散發者是包含散發資料庫的伺服器，而且會儲存所有類型之複寫的中繼資料和記錄資料。 散發者也會儲存異動複寫的交易。 散發者可以是與發行者相同的伺服器 (本機散發者)，也可以是與發行者不同的伺服器 (遠端散發者)。 散發者的角色會視您實作的複寫類型而定。 一般而言，它的角色用於異動複寫的機會，遠大於合併式複寫和快照式複寫。 合併式複寫和快照式複寫通常使用本機散發者，但在非常忙碌的電腦上進行異動複寫時，可以使用遠端散發者提高效益。  
  
 散發者會使用所在伺服器的下列額外資源：  
  
-   如果發行集的快照集檔案儲存於散發者時 (通常是如此)，則會使用額外的磁碟空間。  
  
-   儲存散發資料庫的額外空間。  
  
-   針對在散發者上執行的發送訂閱，複寫代理程式會使用額外處理器資源。  
  
 您選擇作為散發者的伺服器，應該具備足夠的磁碟空間及處理器動力，以便支援該伺服器的複寫及所有其他活動。  
  
## <a name="options"></a>選項。  
 **'\<伺服器名稱>' 將扮演本身的散發者；SQL Server 將建立散發資料庫和記錄**  
 選取此選項即可將您連接的伺服器設定為散發者。  
  
 **使用下列伺服器做為散發者 (注意：您選取的伺服器必須已經設定為散發者)**  
 選取此選項，然後按一下下面的伺服器名稱，即可將其他伺服器設定為散發者。  
  
 **加入**  
 如果沒有列出您要用來作為散發者的伺服器，請按一下 **[加入]** ，以識別該伺服器並將其加入清單。  
  
> [!NOTE]  
>  若要使用遠端伺服器作為散發者，該遠端伺服器必須已經設定為散發者。 執行此精靈的伺服器，在該發行者上必須啟用為散發者。  
  
## <a name="see-also"></a>另請參閱  
 [[設定散發]](configure-distribution.md)   
 [設定發行和散發](configure-publishing-and-distribution.md)  
  
  
