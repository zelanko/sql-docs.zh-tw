---
title: 第1課：建立 Azure 儲存體帳戶和容器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: efdbd930-cde5-41b0-90ad-58a6cc68dddc
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: fbe773b8b8115cafc20bb60e962bfb42c9821636
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75253504"
---
# <a name="lesson-1-create-azure-storage-account-and-container"></a>第1課：建立 Azure 儲存體帳戶和容器
  您必須先建立 Azure 儲存體帳戶和 blob 容器以及共用存取簽章，才能開始在 Azure 儲存體中儲存 SQL Server 的資料檔案。 第1課會逐步引導您登入 Azure 管理入口網站、建立儲存體帳戶、blob 容器，以及共用存取簽章。  
  
 根據預設，只有儲存體帳戶的擁有者可以存取該帳戶內的 Blob、資料表和佇列。 若要能夠在不共用儲存體帳戶存取金鑰的情況下，使用這個新的 SQL Server 增強功能存取這些資源，您需要執行下列操作：  
  
-   將容器的權限設為私用。  
  
-   建立共用存取簽章。 它可讓您藉由指定提供資源的間隔以及用戶端對其擁有的權限，委派容器、Blob、資料表或佇列資源的有限存取權。  
  
-   使用預存的存取原則管理容器或其 Blob 的共用存取簽章。 預存的存取原則為您提供另一種控制共用存取簽章的方法，同時也提供了直接將簽章撤銷的方式。  
  
 如需詳細資訊，請參閱[管理 Azure 儲存體資源的存取](https://msdn.microsoft.com/library/windowsazure/ee393343.aspx)。  
  
## <a name="create-storage-account"></a>建立儲存體帳戶  
 若要在 Azure 管理入口網站上建立儲存體帳戶，請遵循下列步驟：  
  
1.  使用您的帳戶登入[Azure 管理入口網站](https://manage.windowsazure.com)。 如果您沒有 Azure 帳戶，請造訪 [Azure 免費試用](https://www.windowsazure.com/pricing/free-trial/)。  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-1.gif "SQL 14 CTP2")  
  
2.  使用逐步指示來[建立儲存體帳戶](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)。 請注意，建立要用於 Azure 功能中 SQL Server 資料檔案的儲存體帳戶時，您應該取消選取或停用異地複寫。 這是因為無法保證參與地理複寫的多個 Blob 的寫入順序。 如果儲存體帳戶為地理複寫且需要復原，則會發生損毀。  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-2.gif "SQL 14 CTP2")  
  
## <a name="create-a-blob-container"></a>建立 Blob 容器  
 在 Azure 中，容器會提供一組 blob 的群組。 所有 Blob 都必須放在容器中。 儲存體帳戶可以包含不限數目的容器，但是至少必須具有一個容器。 容器可以儲存無限制的 Blob。 如需有關儲存體大小限制的最新資訊，請參閱[如何在 .net 中使用 Azure Blob 儲存體服務](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)。  
  
 若要在 Azure 中建立容器，請遵循下列步驟：  
  
1.  登入 [[Azure 管理入口網站]](https://manage.windowsazure.com)。  
  
2.  選取儲存體帳戶，按一下 [**容器**] 索引標籤，然後按一下畫面底部的 [**新增容器**]，這會開啟新的對話方塊。  
  
3.  輸入容器的名稱。  
  
4.  針對 [**存取類型**] 選取 [**私**用]。 當您將存取權設為 [私用] 時，只有 Azure 帳戶擁有者可以讀取容器和 blob 資料。  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-4.gif "SQL 14 CTP2")  
  
> [!NOTE]  
>  若要以程式設計方式建立容器，您也可以使用 REST 應用程式開發介面。 如需詳細資訊，請參閱[建立容器](https://msdn.microsoft.com/library/windowsazure/dd179468.aspx)和[Azure 儲存體服務 REST API 參考](https://msdn.microsoft.com/library/windowsazure/dd179355.aspx)。  
  
 **下一課：**  
  
 [第2課。在容器上建立原則並產生共用存取簽章 &#40;SAS&#41; 金鑰](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)  
  
