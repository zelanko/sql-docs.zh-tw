---
title: 第 1 課： 建立 Windows Azure 儲存體帳戶和容器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: efdbd930-cde5-41b0-90ad-58a6cc68dddc
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 43489355aabc9c03407dd6b5779996ceef8967b5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48143641"
---
# <a name="lesson-1-create-windows-azure-storage-account-and-container"></a>第 1 課：建立 Windows Azure 儲存體帳戶和容器
  在您開始將 SQL Server 資料檔案儲存在 Windows Azure 儲存體之前，必須先建立 Windows Azure 儲存體帳戶和 Blob 容器以及共用存取簽章。 第 1 課會逐步引導您完成登入 Windows Azure 管理入口網站，以及建立儲存體帳戶、Blob 容器和共用存取簽章的步驟。  
  
 根據預設，只有儲存體帳戶的擁有者才可以存取該帳戶內的 Blob、資料表和佇列。 若要能夠在不共用儲存體帳戶存取金鑰的情況下，使用這個新的 SQL Server 增強功能存取這些資源，您需要執行下列操作：  
  
-   將容器的權限設為私用。  
  
-   建立共用存取簽章。 它可讓您藉由指定提供資源的間隔以及用戶端對其擁有的權限，委派容器、Blob、資料表或佇列資源的有限存取權。  
  
-   使用預存的存取原則管理容器或其 Blob 的共用存取簽章。 預存的存取原則為您提供另一種控制共用存取簽章的方法，同時也提供了直接將簽章撤銷的方式。  
  
 如需詳細資訊，請參閱 <<c0> [ 管理 Windows Azure 儲存體資源的存取](http://msdn.microsoft.com/library/windowsazure/ee393343.aspx)。  
  
## <a name="create-storage-account"></a>建立儲存體帳戶  
 若要在 Windows Azure 管理入口網站上建立儲存體帳戶，請遵循下列步驟：  
  
1.  登入[Windows Azure 管理入口網站](https://manage.windowsazure.com)使用您的帳戶。 如果您沒有 Windows Azure 帳戶，請瀏覽[Windows Azure 免費試用](http://www.windowsazure.com/pricing/free-trial/)。  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-1.gif "SQL 14 CTP2")  
  
2.  使用的逐步指示[建立儲存體帳戶](http://azure.microsoft.com/documentation/articles/storage-create-storage-account/)。 請注意，在建立儲存體帳戶以用於 Windows Azure 功能中的 SQL Server 資料檔案時，您應該取消選取或停用地理複寫。 這是因為無法保證參與地理複寫的多個 Blob 的寫入順序。 如果儲存體帳戶為地理複寫且需要復原，則會發生損毀。  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-2.gif "SQL 14 CTP2")  
  
## <a name="create-a-blob-container"></a>建立 Blob 容器  
 在 Windows Azure 中，容器會提供一組 Blob 的群組。 所有 Blob 都必須位於容器中。 儲存體帳戶可以包含不限數目的容器，但是至少必須具有一個容器。 容器可以儲存不限數目的 Blob。 最新儲存體大小限制的詳細資訊，請參閱[如何在.NET 中使用 Windows Azure Blob 儲存體服務](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)。  
  
 若要在 Windows Azure 中建立容器，請遵循下列步驟：  
  
1.  登入[Windows Azure 管理入口網站](https://manage.windowsazure.com)。  
  
2.  選取儲存體帳戶，請按一下**容器**索引標籤，然後按一下**新增容器**螢幕的底部，這會開啟新的對話方塊。  
  
3.  輸入容器的名稱。  
  
4.  選取 **私人**for**存取類型**。 當您將存取設為私用時，只有 Windows Azure 帳戶擁有者才能讀取容器和 Blob 資料。  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-4.gif "SQL 14 CTP2")  
  
> [!NOTE]  
>  若要以程式設計方式建立容器，您也可以使用 REST 應用程式開發介面。 如需詳細資訊，請參閱 <<c0> [ 建立容器](http://msdn.microsoft.com/library/windowsazure/dd179468.aspx)也[Windows Azure 儲存體服務 REST API 參考](http://msdn.microsoft.com/library/windowsazure/dd179355.aspx)。  
  
 **下一課：**  
  
 [第 2 課：在容器上建立原則，並產生共用存取簽章&#40;SAS&#41;索引鍵](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)  
  
  
