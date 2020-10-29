---
title: 大規模地將 SQL Server 執行個體連線到 Azure Arc
titleSuffix: ''
description: 在本文中，您將了解如何使用服務主體，連線 SQL Server 執行個體作為已啟用 Azure Arc 的 SQL Server (預覽)。
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 0bd60864615e1ffbf2aecac5eb41efa86407ba68
ms.sourcegitcommit: b09f069c6bef0655b47e9953a4385f1b52bada2b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/27/2020
ms.locfileid: "92734379"
---
# <a name="connect-sql-server-instances-to-azure-arc-at-scale"></a>大規模地將 SQL Server 執行個體連線到 Azure Arc

您可以使用[針對單一電腦產生的相同指令碼](connect.md)，將安裝在多部 Windows 或 Linux 電腦上的多個 SQL Server 執行個體連線到 Azure Arc。 指令碼會連線每部電腦，並將其上安裝的 SQL Server 執行個體註冊至 Azure Arc。為了獲得最佳體驗，我們建議使用 Azure Active Directory [服務主體](/azure/active-directory/develop/app-objects-and-service-principals)。 服務主體是特殊的受限管理身分識別，僅可獲得將機器連線至 Azure，以及針對已啟用 Azure Arc 的伺服器和已啟用 Azure Arc 的 SQL Server 建立 Azure資源所需的最小權限。 這是比使用較高權限帳戶 (例如租用戶系統管理員) 更安全的做法，並且遵循我們的存取控制安全性最佳做法。  

用來安裝和設定 Connected Machine 代理程式的安裝方法，需要您使用的自動化方法具有機器的系統管理員權限。 在 Linux 上請使用根帳戶，在 Windows 上則必須是本機系統管理員群組的成員。

開始之前，請務必檢閱[必要條件](overview.md#prerequisites)，並確定您已建立符合必要權限的自訂角色。

## <a name="connecting-multiple-sql-server-instances-on-windows-using-azure-powershell"></a>使用 Azure PowerShell 連線 Windows 上的多個 SQL Server 執行個體

每部電腦都必須安裝 [Azure PowerShell](/powershell/azure/install-az-ps)。

1. 使用 PowerShell 和 [`New-AzADServicePrincipal`](/powershell/module/az.resources/new-azadserviceprincipal) Cmdlet 建立服務主體。 務必將輸出儲存在變數中。 否則，您將無法在稍後取得所需的密碼。

    ```azurepowershell-interactive
    $sp = New-AzADServicePrincipal -DisplayName "Arc-for-servers" -Role <your custom role>
    $sp
    ```

    ```output
    Secret                : System.Security.SecureString
    ServicePrincipalNames : {ad9bcd79-be9c-45ab-abd8-80ca1654a7d1, https://Arc-for-servers}
    ApplicationId         : ad9bcd79-be9c-45ab-abd8-80ca1654a7d1
    ObjectType            : ServicePrincipal
    DisplayName           : Hybrid-RP
    Id                    : 5be92c87-01c4-42f5-bade-c1c10af87758
    Type                  :
    ```

   > [!NOTE]
   > 在建立服務主體時，您的帳戶在要用於上線的訂用帳戶上必須是擁有者或使用者存取系統管理員。 如果您沒有足夠的權限可建立角色指派，服務主體仍可建立，但將無法使機器上線。 [必要權限](overview.md#required-permissions)中會提供如何建立自訂角色的指示。

2. 擷取儲存在 `$sp` 變數中的密碼：

   ```azurepowershell-interactive
   $credential = New-Object pscredential -ArgumentList "temp", $sp.Secret
   $credential.GetNetworkCredential().password
   ```
3. 擷取服務主體的租用戶識別碼值：
 
   ```azurepowershell-interactive
   $tenantId= (Get-AzContext).Tenant.Id
   ```
4. 使用適當的安全性做法複製並儲存密碼、應用程式識別碼和租用戶識別碼值。 如果忘記或遺失服務主體密碼，您可使用 [`New-AzADSpCredential`](/powershell/module/azurerm.resources/new-azurermadspcredential) Cmdlet 加以重設。

   > [!NOTE]
   > 請注意，適用於伺服器的 Azure Arc 目前不支援使用憑證進行登入，因此服務主體必須具有要驗證的秘密。

5. 遵循[將 SQL Server 連線至 Azure Arc](connect.md) 中的指示，從入口網站下載 PowerShell 指令碼。

6. 在 PowerShell ISE 的系統管理執行個體中開啟指令碼，並使用稍早所述的服務主體佈建期間所產生的值來取代下列環境變數。 這些變數一開始是空的。

   ```azurepowershell-interactive
   $servicePrincipalAppId="{serviceprincipalAppID}"
   $servicePrincipalSecret="{serviceprincipalPassword}"
   $servicePrincipalTenantId="{serviceprincipalTenantId}"
   ```

7. 在每部目標電腦上執行指令碼

## <a name="connecting-multiple-sql-server-instances-on-linux-using-azure-cli"></a>使用 Azure CLI 連線 Linux 上的多個 SQL Server 執行個體

每部目的電腦都必須安裝 [Azure CLI](/cli/azure/install-azure-cli)。 如果已提供服務主體認證且沒有其他使用者已經登入，則註冊指令碼會自動以服務主體認證登入 Azure。 使用下列步驟，連線多部 Linux 電腦上的 SQL Server 執行個體。

1. 使用 ['az ad sp create-for-rbac'](/cli/azure/ad/sp#az_ad_sp_create_for_rbac)命令建立服務主體。

   ```azurecli-interactive
   az ad sp create-for-rbac --name <your service principal name> --role <your custom role name>
   ```

   ```output
   { "appId": "d2ff754a-e10a-4eb6-9cdc-ce6e7a4687db",
     "displayName": "Arc-for-servers",
     "name": "http://Arc-for-servers",
     "password": {SomeRandomlyGeneratedPassword}",
     "tenant": "2530e75f-673b-4841-8270-47ca6a34ef4f"
   }
   ```

   > [!NOTE]
   > 在建立服務主體時，您的帳戶在要用於上線的訂用帳戶上必須是擁有者或使用者存取系統管理員。 如果您沒有足夠的權限可建立角色指派，服務主體仍可建立，但將無法使機器上線。 [必要權限](overview.md#required-permissions)中會提供如何建立自訂角色的指示。

2. 遵循[將 SQL Server 連線至 Azure Arc](connect.md) 中的指示，從入口網站下載 Linux Shell 指令碼。

3. 使用 'az ad sp create-for-rbac' 命令所傳回的值來取代指令碼中的下列變數。 這些變數一開始是空的。

   ```bash
   servicePrincipalAppId="{serviceprincipalAppID}"
   servicePrincipalSecret="{serviceprincipalPassword}"
   servicePrincipalTenant="{serviceprincipalTenant}"
   ```

3. 在每部目標電腦上執行指令碼
 
   ```bash
   sudo chmod +x ./RegisterSqlServerArc.sh
   ./RegisterSqlServerArc.sh
   ```

## <a name="validate-successful-onboarding"></a>驗證上線是否成功

在您向已啟用 Azure Arc 的 SQL Server (預覽) 註冊 SQL Server 執行個體後，請移至 [Azure 入口網站](https://aka.ms/azureportal)並檢視新建立的 Azure Arc 資源。 您會看到每部連線的電腦有新的 [電腦 - Azure Arc]，以及每個已註冊的 SQL Server 執行個體有新的 [SQL Server - Azure Arc] 資源。 

![成功上線](./media/join-at-scale/successful-onboard.png)

## <a name="next-steps"></a>後續步驟

- 了解如何使用 [Azure 原則](/azure/governance/policy/overview)，針對例如 VM [來賓設定](/azure/governance/policy/concepts/guest-configuration)、確認機器回報至預期的 Log Analytics 工作區、使用 [Azure 監視器與 VM](/azure/azure-monitor/insights/vminsights-enable-policy) 啟用監視等等項目，管理您的機器。

- 深入了解 [Log Analytics 代理程式](/azure/azure-monitor/platform/log-analytics-agent)。 您需要適用於 Windows 和 Linux 的 Log Analytics 代理程式來主動監視機器上執行的作業系統和工作負載、使用自動化 Runbook 或解決方案 (例如更新管理) 來管理機器，或使用其他 Azure 服務 (例如 [Azure 資訊安全中心](/azure/security-center/security-center-intro))。

- 了解如何[使用隨選 SQL 評量來設定您的 SQL Server 執行個體以進行定期環境健康情況檢查](assess.md)

- 了解如何[設定 SQL Server 執行個體的進階資料安全性](configure-advanced-data-security.md)