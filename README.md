
# Ingress Endpoint Helm Chart

このHelm Chartは、既存のKubernetesサービスに対して**シンプルなIngressエンドポイント**をデプロイすることを目的としています。アプリケーションのPodやServiceは含まず、純粋にトラフィックルーティングのためのIngressリソースのみを提供します。

## 🚀 概要

Kubernetes環境において、既存のバックエンドサービスに外部からアクセスするためのIngressリソースを迅速に作成したい場合に最適です。このChartは、以下のようなシナリオで役立ちます。

  * 既にデプロイ済みのアプリケーションにIngressルールを追加したい場合。
  * 他のHelm Chartや手動でデプロイされたServiceにIngressを設定したい場合。
  * 特定のホスト名やパスに対するシンプルなルーティングを管理したい場合。

## ✨ 特徴

  * **Ingressリソースのみ**: アプリケーションのDeploymentやServiceはデプロイしません。
  * **柔軟な設定**: ホスト名、パス、バックエンドサービス、TLS設定などを `values.yaml` で簡単にカスタマイズ可能。
  * **汎用性**: 特定のアプリケーションに依存せず、既存のどのServiceにも適用可能。

## 📚 前提条件

  * Kubernetesクラスター (v1.19以上を推奨)
  * Helm (v3.0以上)
  * クラスター内に**Ingress Controller**がインストールされていること (例: NGINX Ingress Controller, Traefik, AWS ALB Ingress Controllerなど)。

## 📦 インストール

以下の手順でChartをインストールします。

1.  **リポジトリをクローンする**:

    ```bash
    git clone https://github.com/devnekoops/ingress-endpoint.git
    cd ingress-endpoint
    ```

2.  **`values.yaml` をカスタマイズする**:
    Chartの動作を設定するため、`values.yaml` ファイルを編集します。少なくとも、`ingress.host` と `ingress.serviceName` は設定してください。

    ```yaml
    # values.yaml の例
    ingress:
      enabled: true
      className: "nginx" # 使用するIngressClass名。環境に合わせて変更してください。
      host: "your-domain.com" # 必須: Ingressのホスト名
      path: "/"
      pathType: Prefix
      serviceName: "your-backend-service" # 必須: トラフィックを転送する既存のService名
      servicePort: 80 # 必須: 上記Serviceのポート
      annotations: {} # 必要に応じてIngressのアノテーションを追加
      tls:
        enabled: false # TLSを有効にする場合は true に設定
        secretName: "" # TLS証明書を格納したSecret名（例: my-tls-secret）
        hosts: [] # TLSを使用するホスト名のリスト（例: ["your-domain.com"]）
    ```

3.  **Helm Chartをインストールする**:
    `my-ingress` は任意のリリース名です。

    ```bash
    helm install my-ingress . -f values.yaml
    ```

## 🛠️ アンインストール

Chartのリリースを削除するには、以下のコマンドを実行します。

```bash
helm uninstall my-ingress
```

これにより、デプロイされたIngressリソースがクラスターから削除されます。

## ⚙️ 設定

`values.yaml` を使用して、Chartの様々な設定をカスタマイズできます。

| パラメータ                | 説明                                      | デフォルト     |
| :---------------------- | :---------------------------------------- | :------------- |
| `ingress.enabled`       | Ingressリソースを有効にするかどうか       | `true`         |
| `ingress.className`     | 使用するIngressClassの名前                | `"nginx"`      |
| `ingress.host`          | Ingressに設定するホスト名                 | `""`           |
| `ingress.path`          | ルーティングするパス                      | `"/"`          |
| `ingress.pathType`      | パスのマッチングタイプ (Prefix, Exact, ImplementationSpecific) | `Prefix`       |
| `ingress.serviceName`   | トラフィックを転送する既存のKubernetes Serviceの名前 | `""`           |
| `ingress.servicePort`   | 上記Serviceのポート番号                   | `80`           |
| `ingress.annotations`   | Ingressリソースに追加するアノテーション | `{}`           |
| `ingress.tls.enabled`   | TLSを有効にするかどうか                   | `false`        |
| `ingress.tls.secretName`| TLS証明書を格納したKubernetes Secretの名前 | `""`           |
| `ingress.tls.hosts`     | TLSを使用するホスト名のリスト             | `[]`           |

## 🤝 貢献

このChartの改善にご協力いただける方を歓迎します。バグ報告、機能リクエスト、プルリクエストなど、お気軽にお寄せください。

## 📄 ライセンス

このプロジェクトは [Apache 2.0 License](https://www.google.com/search?q=https://github.com/devnekoops/ingress-endpoint/blob/main/LICENSE) の下でライセンスされています。

-----
-----

# Ingress Endpoint Helm Chart

[](https://www.google.com/search?q=https://github.com/devnekoops/ingress-endpoint/blob/main/LICENSE)
[](https://github.com/devnekoops/ingress-endpoint)

This Helm Chart is designed to deploy a **simple Ingress endpoint** for existing Kubernetes services. It does not include application Pods or Services, providing only the Ingress resource for traffic routing.

## 🚀 Overview

This chart is perfect for quickly creating an Ingress resource to expose an existing backend service to external traffic in your Kubernetes environment. It's useful in scenarios like:

  * Adding Ingress rules to an already deployed application.
  * Setting up Ingress for Services deployed via other Helm charts or manually.
  * Managing simple routing for specific hostnames or paths.

## ✨ Features

  * **Ingress Resource Only**: It doesn't deploy application Deployments or Services.
  * **Flexible Configuration**: Easily customize hostname, path, backend service, and TLS settings via `values.yaml`.
  * **Versatile**: Not tied to a specific application; can be applied to any existing Service.

## 📚 Prerequisites

  * A Kubernetes cluster (v1.19+ recommended).
  * Helm (v3.0+).
  * An **Ingress Controller** must be installed in your cluster (e.g., NGINX Ingress Controller, Traefik, AWS ALB Ingress Controller).

## 📦 Installation

Follow these steps to install the chart:

1.  **Clone the repository**:

    ```bash
    git clone https://github.com/devnekoops/ingress-endpoint.git
    cd ingress-endpoint
    ```

2.  **Customize `values.yaml`**:
    Edit the `values.yaml` file to configure the chart's behavior. At a minimum, set `ingress.host` and `ingress.serviceName`.

    ```yaml
    # Example values.yaml
    ingress:
      enabled: true
      className: "nginx" # IngressClass name to use. Change according to your environment.
      host: "your-domain.com" # Required: Hostname for the Ingress
      path: "/"
      pathType: Prefix
      serviceName: "your-backend-service" # Required: Name of the existing Service to forward traffic to
      servicePort: 80 # Required: Port of the above Service
      annotations: {} # Add Ingress annotations as needed
      tls:
        enabled: false # Set to true to enable TLS
        secretName: "" # Name of the Kubernetes Secret containing the TLS certificate (e.g., my-tls-secret)
        hosts: [] # List of hostnames to use TLS for (e.g., ["your-domain.com"])
    ```

3.  **Install the Helm Chart**:
    `my-ingress` is an arbitrary release name.

    ```bash
    helm install my-ingress . -f values.yaml
    ```

## 🛠️ Uninstallation

To delete the chart release, run the following command:

```bash
helm uninstall my-ingress
```

This will remove the deployed Ingress resource from your cluster.

## ⚙️ Configuration

You can customize various chart settings using `values.yaml`.

| Parameter               | Description                               | Default        |
| :---------------------- | :---------------------------------------- | :------------- |
| `ingress.enabled`       | Whether to enable the Ingress resource    | `true`         |
| `ingress.className`     | Name of the IngressClass to use           | `"nginx"`      |
| `ingress.host`          | Hostname for the Ingress                  | `""`           |
| `ingress.path`          | Path to route                             | `"/"`          |
| `ingress.pathType`      | Path matching type (Prefix, Exact, ImplementationSpecific) | `Prefix`       |
| `ingress.serviceName`   | Name of the existing Kubernetes Service to forward traffic to | `""`           |
| `ingress.servicePort`   | Port number of the above Service          | `80`           |
| `ingress.annotations`   | Annotations to add to the Ingress resource | `{}`           |
| `ingress.tls.enabled`   | Whether to enable TLS                     | `false`        |
| `ingress.tls.secretName`| Name of the Kubernetes Secret containing the TLS certificate | `""`           |
| `ingress.tls.hosts`     | List of hostnames to use TLS for          | `[]`           |

## 🤝 Contributing

Contributions to improve this chart are welcome. Feel free to submit bug reports, feature requests, or pull requests.

## 📄 License

This project is licensed under the Apache 2.0 License.
