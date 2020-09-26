---
title: 使用 Azure Data Studio 部署 Azure SQL Edge
description: 如何在 Azure Data Studio 中部署 Azure SQL Edge 執行個體
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: 89732af2b2fc5926193519b4a6508b97ac998c88
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364115"
---
# <a name="deploy-azure-sql-edge-with-azure-data-studio-preview"></a>使用 Azure Data Studio 部署 Azure SQL Edge (預覽)

[Azure SQL Edge](https://docs.microsoft.com/azure/azure-sql-edge/overview) 是專為 IoT 和 Azure IoT Edge 部署而最佳化的關聯式資料庫引擎。 其功能可為 IoT 應用程式和解決方案建立高效能的資料儲存和處理層。 本文說明如何使用 Azure Data Studio 部署 Azure SQL Edge 執行個體，以及部署精靈支援的部署案例。  

Azure Data Studio 中的部署精靈支援下列案例：

- 本機容器執行個體
- 遠端容器執行個體
- 新的 Azure IoT 中樞和 VM
- Azure IoT 中樞的現有裝置
- Azure IoT 中樞的多個裝置

| 必要工具 | `Docker` | `Azure CLI` |
| ------------- | :---: | :---: |
| 本機容器執行個體 | x | |
| 遠端容器執行個體 | | |
| 新的 Azure IoT 中樞和 VM | | x |
| Azure IoT 中樞的現有裝置 |  | x |
| Azure IoT 中樞的多個裝置 |   |  x |

> [!NOTE]
> Azure SQL Edge 部署 (預覽) 可透過延伸模組「Azure SQL Edge 部署延伸模組」取得，而這些功能目前為預覽狀態。 若要讓這些功能可供您使用，請在 Azure Data Studio 中安裝延伸模組。

若要開始在 Azure Data Studio 中部署，請開啟 [連線] 檢視中的功能表，然後選取 [新增部署...] 選項。  針對所有 Azure SQL Edge 案例，在以下畫面上選取 [Azure SQL Edge]，並從 [部署目標] 下拉式清單中選擇所需的案例。 部署精靈會產生可執行的 TSQL 筆記本來完成部署。 請注意，連線資訊 (包括 SQL 系統管理員密碼) 預設會包含在筆記本中。

![部署概觀](media/deploy-azure-sql-edge/deploy-overview.png)

## <a name="local-container-instance"></a>本機容器執行個體

藉由指定容器名稱、`sa` 使用者密碼和適用於 Azure SQL Edge 連線的主機連接埠，即可將 Azure SQL Edge 部署至 localhost 上的 Docker 容器。  完成部署之後，筆記本底部有數個連結可供採取進一步動作：

- **選取這裡以連線到 Azure SQL Edge 執行個體**：在 Azure Data Studio 中建立連到新 Azure SQL Edge 執行個體的連線
- **開啟終端機視窗**：在 Azure Data Studio 中開啟終端機 (現有或新的)
- **停止容器**：將命令複製到終端機，以在使用者執行時停止容器
- **移除容器**：將命令複製到終端機，以在使用者執行時移除容器

## <a name="remote-container-instance"></a>遠端容器執行個體

藉由指定容器資訊和目標/主機電腦資訊，即可將 Azure SQL Edge 部署到已安裝 Docker 的遠端主機上的 Docker 容器。  完成部署之後，可以在筆記本底部取得連線連結。  由於遠端容器主機環境的緣故，若要停止或移除容器，則必須複製命令以在遠端 Shell 中執行。

## <a name="new-azure-iot-hub-and-vm"></a>新的 Azure IoT 中樞和 VM

Azure SQL Edge 部署精靈可以建立數個 Azure 資源，以便部署連線至 Azure IoT 中樞並已啟用 Edge 的虛擬機器 (VM)。 需要有效的 Azure 訂用帳戶。 此部署會建立：

- 資源群組 (如果未選取目前的資源群組)
- 網路安全性群組
- 虛擬機器
- 靜態公用 IP 位址

(選擇性) dacpac 檔案可以壓縮在資料夾中並部署到新的 Azure SQL Edge 執行個體作為此程序的一部分。  如果提供 dacpac 檔案，就會在相同的資源群組中建立 Azure Blob 儲存體帳戶。

## <a name="existing-device-of-an-azure-iot-hub"></a>Azure IoT 中樞的現有裝置

如果您有現有的 IoT 中樞和已連線的裝置，則可根據資源群組、IoT 中樞名稱和裝置識別碼，將 Azure SQL Edge 部署至裝置。
在部署精靈期間提供的 IP 位址用於在筆記本底部產生快速連線連結。

(選擇性) dacpac 檔案可以壓縮在資料夾中並部署到新的 Azure SQL Edge 執行個體作為此程序的一部分。  如果提供 dacpac 檔案，就會在相同的資源群組中建立 Azure Blob 儲存體帳戶。

## <a name="multiple-devices-of-an-azure-iot-hub"></a>Azure IoT 中樞的多個裝置

如果您有現有的 IoT 中樞和已連線的裝置，則可根據資源群組、IoT 中樞名稱，以及要選取裝置的[目標條件](https://docs.microsoft.com/azure/iot-edge/module-deployment-monitoring#target-condition)，將 Azure SQL Edge 部署至裝置。
在部署精靈期間提供的 IP 位址用於在筆記本底部產生快速連線連結。

(選擇性) dacpac 檔案可以壓縮在資料夾中並部署到新的 Azure SQL Edge 執行個體作為此程序的一部分。  如果提供 dacpac 檔案，就會在相同的資源群組中建立 Azure Blob 儲存體帳戶。

## <a name="next-steps"></a>下一步

- [深入了解 Azure SQL Edge](https://docs.microsoft.com/azure/azure-sql-edge/)