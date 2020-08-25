---
title: SQL Server 中央管理伺服器延伸模組
description: 了解如何安裝和使用 SQL Server 中央管理伺服器延伸模組 (預覽)，這是一種用於將伺服器分組，並套用動作至群組的延伸模組。
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.custom: seodec18
ms.date: 06/06/2019
ms.openlocfilehash: 3024a9c61fb51063b50f8fde769e7bdbb5608fbf
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766047"
---
# <a name="sql-server-central-management-servers-extension-preview"></a>SQL Server 中央管理伺服器延伸模組 (預覽)

中央管理伺服器延伸模組可讓使用者儲存一份 SQL Server 執行個體清單，其會組織為一或多個群組。 使用 CMS 群組所採取的動作，將會在伺服器群組中的所有伺服器上運作。

此體驗目前為初始預覽狀態。 請在[這裡](https://github.com/microsoft/azuredatastudio/issues)回報問題和功能要求。

![CMS 延伸模組](media/sql-server-cms-extension/cms-list.png)

## <a name="install-the-sql-server-central-management-servers-extension"></a>安裝 SQL Server 中央管理伺服器延伸模組

1. 若要開啟延伸模組管理員並存取可用的延伸模組，請選取延伸模組圖示，或選取 [檢視] 功能表中的 [延伸模組]。
2. 選取可用的延伸模組，檢視詳細資料。
1. 選取您想要的延伸模組 (SQL Server 中央管理伺服器) 並加以**安裝**。

### <a name="how-do-i-start-central-management-servers"></a>如何啟動中央管理伺服器？
 按一下連線圖示 (Ctrl/Cmd + G) 即可檢視中央管理伺服器。 第一次下載延伸模組時，CMS 檢視會最小化，您可以按一下 [中央管理伺服器]  加以開啟

## <a name="next-steps"></a>後續步驟
若要深入了解中央管理伺服器概念，[您可以在這裡閱讀詳細資訊](../ssms/register-servers/create-a-central-management-server-and-server-group.md)。