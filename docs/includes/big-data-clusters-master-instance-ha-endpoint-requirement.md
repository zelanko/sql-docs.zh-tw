---
ms.openlocfilehash: 497a564a10a3d35b33f47222fce8f89fe36bd15e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73530936"
---
特定作業需要連接到 SQL Server 執行個體，包括設定伺服器 (執行個體層級) 或手動將資料庫新增至可用性群組。 `sp_configure`、`RESTORE DATABASE` 等作業，或可用性群組所屬資料庫中的任何 DDL 命令，都需要連接到 SQL Server 執行個體。 根據預設，巨量資料叢集不含可連接到執行個體的端點。 您必須手動公開此端點。

如需指示，請參閱[連接到主要複本上的資料庫](../big-data-cluster/deployment-high-availability.md#instance-connect)。