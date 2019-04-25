---
title: 連接已註冊的伺服器和物件總管 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: d6b3911f-68b4-4483-831b-df89d6400add
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 374d75c18adc091eaf6a01ae1164a529a34accee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62636422"
---
# <a name="connect-with-registered-servers-and-object-explorer"></a>連接已註冊的伺服器和物件總管
  本教學課程示範已註冊的伺服器和物件總管的用法。  
  
 本教學課程會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。 為了加強安全性，依預設，不會安裝範例資料庫。 如需詳細資訊，請參閱 [安裝 SQL Server 範例和範例資料庫](http://sqlserversamples.codeplex.com)。  
  
## <a name="connecting-to-servers"></a>連接到伺服器  
 已註冊之伺服器元件的工具列有 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的按鈕。 您可以註冊其中一種或多種伺服器類型，以便於管理。 嘗試下列練習，以註冊 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
#### <a name="to-register-the-database"></a>註冊資料庫  
  
1.  必要的話，在 [已註冊的伺服器] 工具列上，按一下 [Database Engine] (可能已選取它)。  
  
2.  展開 [Database Engine]。  
  
3.  以滑鼠右鍵按一下 [本機伺服器群組]，然後按一下 [新增伺服器註冊]。  
  
4.  在 [新增伺服器註冊] 對話方塊的 [伺服器名稱] 文字方塊中，輸入您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。  
  
5.  在 [已註冊的伺服器名稱] 方塊中，輸入 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]。  
  
6.  在 **連接屬性**索引標籤**連接到資料庫**清單中，選取**\<瀏覽伺服器...> >**。  
  
7.  在 [瀏覽資料庫] 對話方塊中，按一下 [是]。  
  
8.  在 [瀏覽伺服器上的資料庫] 對話方塊中，選取 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，然後按一下 [確定]。  
  
9. 若要驗證伺服器已正確地註冊，請按一下 [測試]。  
  
10. 在 [新增伺服器註冊] 對話方塊中，按一下 [儲存]。  
  
## <a name="connecting-with-object-explorer"></a>連接物件總管  
 如同已註冊的伺服器，[物件總管] 也可以連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
#### <a name="to-connect-with-object-explorer"></a>連接物件總管  
  
1.  在物件總管的工具列上，按一下 [連接] 列出可能的連接類型，然後選取 [Database Engine]。  
  
2.  在 [連接到伺服器] 對話方塊的 [伺服器名稱] 文字方塊中，輸入您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。  
  
3.  按一下 [選項]，瀏覽所提供選擇。  
  
4.  若要連接到伺服器，請按一下 [連接]。 如果已連接，此動作就會讓您返回 [物件總管]，並將焦點設在該伺服器上。  
  
     您可以利用 [物件總管] 來管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent、複寫和 Database Mail。 [物件總管] 只能管理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssIS](../../includes/ssis-md.md)]的部分功能。 這些元件每個都有其他專用工具。  
  
5.  在物件總管中，展開 [資料庫] 資料夾，然後選取 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]。  
  
     請注意，[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會在另外一個資料夾中提供系統資料庫。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [變更環境配置](lesson-1-3-change-the-environment-layout.md)  
  
  
