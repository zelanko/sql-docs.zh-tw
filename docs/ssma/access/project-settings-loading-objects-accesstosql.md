---
description: '專案設定 (載入物件)  (AccessToSQL) '
title: 專案設定 (載入物件)  (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9ec1c1e8-a3e1-4e81-bf49-631f87daa209
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: f03b7457d79c573806ffbda2b601f56d0f942a54
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488199"
---
# <a name="project-settings-loading-objects-accesstosql"></a>專案設定 (載入物件)  (AccessToSQL) 
[載入物件] 專案設定可讓您設定 Access 資料庫物件與 SQL Server 資料庫物件同步處理的方式。  
  
預設動作會指定從 Access 資料庫重新整理物件，以及同步處理物件與 SQL Server 資料庫的預設設定。 如需詳細資訊，請參閱 [從資料庫重新整理 &#40;AccessToSQL&#41;](../../ssma/access/refresh-from-database-accesstosql.md)  
  
您可以存取兩個不同的同步處理頁面，其中包含相同的設定：  
  
-   若要指定所有未來 SSMA 專案的設定，請按一下 [ **工具** ] 功能表上的 [ **DefaultProject 設定**]，然後按一下左窗格底部的 [ **載入物件** ]。  
  
-   若要指定目前專案的設定，請按一下 [ **工具** ] 功能表上的 [ **專案設定**]，然後按一下左窗格底部的 [ **載入物件** ]。  
  
## <a name="options"></a>選項。  
  
##### <a name="misc"></a>其他  
  
##### <a name="attempts"></a>嘗試  
提供載入 SQL Server 所需的傳遞物件數目的相關資訊。 將物件載入 SQL Server 通常會在多個階段中執行。 無法在第一次傳遞中載入的物件（例如外鍵）可能會在下一次成功時成功載入。  
  
預設值為2。  
  
## <a name="synchronization-for-sql-server"></a>SQL Server 的同步處理  
  
##### <a name="default-action-on-local-and-remote-object-change"></a>本機和遠端物件變更的預設動作  
當物件定義在 SSMA 和資料庫伺服器上變更時，指定 [同步處理] 對話方塊中的預設設定。  
  
-   如果您選取 [ **從資料庫**重新整理]，SSMA 會在符合條件時將資料庫定義載入中繼資料。  
  
-   如果您選取 [ **寫入資料庫**]，SSMA 會在符合條件時，根據 SSMA 中繼資料內容來更新資料庫中的物件。  
  
-   如果您選取 [ **略過**]，SSMA 將不會執行任何重新整理動作。  
  
##### <a name="default-action-on-local-object-change"></a>本機物件變更的預設動作  
當物件在 SSMA 中變更時，請在 [同步處理] 對話方塊中指定預設設定。  
  
-   如果您選取 [ **從資料庫**重新整理]，SSMA 會在符合條件時將資料庫定義載入中繼資料。  
  
-   如果您選取 [ **寫入資料庫**]，SSMA 會在符合條件時，根據 SSMA 中繼資料內容來更新資料庫中的物件。  
  
-   如果您選取 [ **略過**]，SSMA 將不會執行任何重新整理動作。  
  
##### <a name="default-action-on-remote-object-change"></a>遠端物件變更的預設動作  
當物件在資料庫伺服器上變更時，請在 [同步處理] 對話方塊中指定預設設定。  
  
-   如果您選取 [ **從資料庫**重新整理]，SSMA 會在符合條件時將資料庫定義載入中繼資料。  
  
-   如果您選取 [ **寫入資料庫**]，SSMA 會在符合條件時，根據 SSMA 中繼資料內容來更新資料庫中的物件。  
  
-   如果您選取 [ **略過**]，SSMA 將不會執行任何重新整理動作。  
  
##### <a name="default-action-when-local-object-metadata-is-missing"></a>缺少區域物件中繼資料時的預設動作  
當缺少區域中繼資料時，指定 [同步處理] 對話方塊中的預設設定。  
  
-   如果您選取 [ **從資料庫**重新整理]，SSMA 會在符合條件時選取 [從資料庫重新整理] 選項。  
  
-   如果您選取 [ **寫入資料庫**]，則當符合條件時，SSMA 會從資料庫中刪除物件。  
  
-   如果您選取 [ **略過**]，SSMA 將不會執行任何重新整理動作。  
  
