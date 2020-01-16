---
title: チュートリアル:Azure portal を使用して Azure Firewall のデプロイと構成を行う
description: このチュートリアルでは、Azure portal を使用して Azure Firewall をデプロイおよび構成する方法を学習します。
services: firewall
author: vhorne
ms.service: firewall
ms.topic: tutorial
ms.date: 10/28/2019
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: be39449c1c11acdbdc99bd96f917c51eebda44ae
ms.sourcegitcommit: 8e31a82c6da2ee8dafa58ea58ca4a7dd3ceb6132
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2019
ms.locfileid: "74195789"
---

アウトバウンド ネットワーク アクセスを制御することは、ネットワーク セキュリティ プラン全体の重要な要素です。 たとえば、Web サイトへのアクセスを制限することができます。 また、アクセスできるアウトバウンドの IP アドレスとポートを制限することもできます。


Azure サブネットから外に向かうアウトバウンド ネットワーク アクセスを制御する方法の 1 つとして、Azure Firewall の使用が挙げられます。 Azure Firewall を使用して、次のルールを構成できます。

* アプリケーション ルール: サブネットからアクセスできる完全修飾ドメイン名 (FQDN) を定義します。
* ネットワーク ルール: 送信元アドレス、プロトコル、宛先ポート、送信先アドレスを定義します。
www.google.com コル、宛先ポート、送信先ア。

 ネットワーク トラフィックは、サブネットの既定ゲートウェイとしてのファイアウォールにルーティングしたときに、構成されているファイアウォール ルールに制約されます。

 www.google.com このチュートリアルでは、デプロイしやすいよう単純化して、3 つのサブネットを含んだ単一の VNet を作成します。 運用環境のデプロイでは、[ハブとスポーク モデル](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)を採用して、独自の VNet にファイアウォールを配置することをお勧めします。 ワークロード サーバーは、1 つ以上のサブネットを含む同じリージョンのピアリングされた VNet に配置されます。

http://portal.azure.com * **AzureFirewallSubnet** - このサブネットにファイアウォールが存在します。
* **Workload-SN** - このサブネットにはワークロード サーバーがあります。 このサブネットのネットワーク トラフィックは、ファイアウォールを通過します。
* **Jump-SN** - このサブネットには "ジャンプ" サーバーがあります。 ジャンプ サーバーには、リモート デスクトップを使用して接続できるパブリック IP ア ドレスがあります。 そこから、(別のリモート デスクトップを使用して) ワークロード サーバーに接続できます。

![チュートリアルのネットワーク インフラストラクチャ](media/tutorial-firewall-rules-portal/Tutorial_network.png)。

 http://portal.azure.com  このチュートリアルでは、以下の内容を学習します。
