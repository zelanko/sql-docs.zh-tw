---
author: MikeRayMSFT
ms.prod: sql
ms.technology: big-data-cluster
ms.topic: include
ms.date: 06/22/2020
ms.author: mikeray
ms.openlocfilehash: b72f8044638adbf75049392fae32447a8a749a6d
ms.sourcegitcommit: d973b520f387b568edf1d637ae37d117e1d4ce32
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85215064"
---
從 SQL Server 2019 CU5 開始，當您使用基本驗證部署新的叢集時，所有端點 (包括閘道) 都會使用 `AZDATA_USERNAME` 和 `AZDATA_PASSWORD`。 升級至 CU5 的叢集上的端點會繼續使用 `root` 作為使用者名稱，以連線至閘道端點。 這項變更不適用於使用 Active Directory 驗證的部署。 請參閱版本資訊中的[透過閘道端點存取服務的認證](../big-data-cluster/release-notes-big-data-cluster.md#credentials-for-accessing-services-through-gateway-endpoint)。