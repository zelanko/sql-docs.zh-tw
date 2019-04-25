---
layout: HubPage
hide_bc: true
title: SQL Server 安全性
description: 探索可讓 SQL Server 保持安全的功能。
ms.topic: hub-page
ms.prod: sql
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.date: 12/15/2018
featureFlags:
- clicktale
ms.openlocfilehash: f1b88c2a82866c171601d5184a90fd0d6362a435
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213565"
---
<div id="main" class="v2">
    <div class="container">
        <ul class="cardsY panelContent featuredContent">
            <li>
                <a href="https://www.microsoft.com/evalcenter/evaluate-sql-server-2019-ctp">
                    <div class="cardSize">
                        <div class="cardPadding">
                            <div class="card">
                                <div class="cardImageOuter">
                                    <div class="cardImage">
                                        <img src="media/index/download-sql-server.svg" alt="" />
                                    </div>
                                </div>
                                <div class="cardText">
                                    <span class="likeAnH3">試用 SQL Server 2019 (預覽)</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </li>
            <li>
                <a href="https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm">
                    <div class="cardSize">
                        <div class="cardPadding">
                            <div class="card">
                                <div class="cardImageOuter">
                                    <div class="cardImage">
                                        <img src="media/index/get-azure-sql-vm.svg" alt="" />
                                    </div>
                                </div>
                                <div class="cardText">
                                    <span class="likeAnH3">取得含 SQL Server 的虛擬機器</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </li>
            <li>
                <a href="/sql/ssms/download-sql-server-management-studio-ssms">
                    <div class="cardSize">
                        <div class="cardPadding">
                            <div class="card">
                                <div class="cardImageOuter">
                                    <div class="cardImage">
                                        <img src="media/index/download-ssms.svg" alt="" />
                                    </div>
                                </div>
                                <div class="cardText">
                                    <span class="likeAnH3">下載 SQL Server Management Studio</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </li>              
        </ul>
    </div>
    <div class="container">
        <h1>保護 SQL Server</h1>
        <ul class="pivots tabLess">
            <li class="pivotItem" style="display: list-item;" data-id="#products">
                <a href="#products" data-linktype="self-bookmark"></a>
                <ul id="products">
                    <li class="panelItem" data-index="0">
                        <a class="singlePanelNavItem selected" href="#products1" data-linktype="self-bookmark"></a>
                        <ul class="cardsD panelContent singlePanelContent" id="products1" style="margin-top: 0px; display: flex;">
                            <li>
                                <a href="/sql/relational-databases/security/authentication-access/managing-logins-users-and-schemas-how-to-topics/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/secure-sql-server/access-management.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>存取管理</h3>
                                                    <p>管理登入、使用者與結構描述。 </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/security/encryption/always-encrypted-database-engine/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img  src="media/secure-sql-server/always-encrypted.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Always Encrypted</h3>
                                                    <p>可讓用戶端將用戶端應用程式內的敏感性資料加密，且絕對不會向資料庫引擎透露金鑰。 </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/security/dynamic-data-masking/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img  src="media/secure-sql-server/dynamic-data-masking.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>動態資料遮罩</h3>
                                                    <p>對不具權限的使用者遮罩敏感性資料，以限制其曝光。 </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/security/permissions-database-engine/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img  src="media/secure-sql-server/permissions.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>權限</h3>
                                                    <p>決定哪些人具有存取 SQL Server 內容的權限。 </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/security/row-level-security/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img  src="media/secure-sql-server/row-level-security.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>資料列層級安全性</h3>
                                                    <p>以執行查詢之使用者的特性為基礎，啟用對資料庫資料表中資料列的存取。</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/connect/jdbc/understanding-ssl-support/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img  src="media/secure-sql-server/ssl.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>安全通訊端層 (SSL)</h3>
                                                    <p>在過程中加密資料。</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/security/encryption/transparent-data-encryption">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img  src="media/secure-sql-server/tde.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>透明資料加密 (TDE)</h3>
                                                    <p>加密磁碟上的待用資料。 </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                        </ul>
                    </li>
                </ul>
            </li>
        </ul>
    </div>
</div>
<div class="container centered pageFooter">
        <h2>與我們保持連絡</h2>
        <ul class="links">
           <li>
                <a href="https://aka.ms/editsqldocs" data-linktype="external"> 參與 </a>
            </li>
           <li>
                <a href="https://docs.microsoft.com/sql/sql-server/sql-server-get-help" data-linktype="external"> 取得協助 </a>
            </li>
           <li>
                <a href="https://aka.ms/sqldocsfeedback" data-linktype="external"> 意見反應 </a>
            </li>
           <li>
                <a href="https://aka.ms/sqldocsurvey" data-linktype="external"> 問卷 </a>
            </li>
           <li>
                <a href="https://cloudblogs.microsoft.com/sqlserver/" data-linktype="external">部落格</a>
            </li>
            <li>
                <a href="https://twitter.com/sqldocs" data-linktype="external">Twitter</a>
            </li>
            <li>
                <a href="https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqldatabaseengine&filter=alltypes&sort=lastpostdesc" data-linktype="external">MSDN 論壇</a>
            </li>
            <li>
                <a href="https://feedback.azure.com/forums/908035-sql-server" data-linktype="external">User Voice</a>
            </li>
        </ul>
    </div>
