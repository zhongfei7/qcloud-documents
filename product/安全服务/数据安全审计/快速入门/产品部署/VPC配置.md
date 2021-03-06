CDS-Audit 部署的核心目标是把 Agent 安装到数据库服务器中，并且确保数据库服务器与 CDS-Audit 审计实例能实现网络连通，实现该目标需要进行 VPC 配置和 [Agent 部署](https://cloud.tencent.com/document/product/856/17385)。
为确保您的 VPC 自主可控，我们不会对您的 VPC 做任何自动化修改，因此需要您手动配置 VPC 参数。配置 VPC 需要配置 “对等网络” 和 “路由表” 两个选项，以实现 VPC 网络和 CDS-Audit 所属 VPC 的网络互通，其操作步骤如下图所示：
![0](https://main.qcloudimg.com/raw/5fad24debe5db784b0a5a9066dbf85d4.png)
下面将为您详细介绍操作步骤。
## 进入私有网络配置页面
登录 [腾讯云控制台](https://console.cloud.tencent.com/)，选择【云产品】>【私有网络】进入私有网络控制台。
## 配置对等网络
1. 在左侧导航中单击【对等连接】进入配置页面。
 ![1](https://main.qcloudimg.com/raw/517a59aacb75ee6eac2c50b07ff49d3a.png)
2. 单击 【新建】，填写配置信息，配置项填写说明如下：
 - 名称：任意填写简单易记的名称即可（如 test）；
 - 本端地域：选择本端数据库服务器所处的地域；
 - 本端网络：选择本端数据库服务器所处的私有网络。当您从未新建过私有网络时，本配置仅一个选项，选择这个唯一选项即可；
 - 对端账户类型：选择其他账户
 - 对端地域：选择您购买的数盾数据安全审计实例所处地域，注意地域如果不在同一区域需要额外费用；
 - 对端账户：固定填写 `100005260334`；
 - 对端网络：固定填写 `vpc-7qxgvesv`。
 ![2](https://main.qcloudimg.com/raw/91f6bc95ef9abd55dcaf2b21aea9ea19.png)
3. 配置完毕后，单击【创建】即可完成配置。

## 配置路由表
配置完对等网络后，我们开始配置 “路由表”。
1. 同样在私有网络界面左侧导航单击 【路由表】进入配置页面。
 ![3](https://main.qcloudimg.com/raw/c19ff4c88fd5bec52484b7a2446789e3.png)
2. 单击【新建】，填写配置信息，配置项填写说明如下：
 - 名称：任意填写简单易记的名称即可；
 - 所属网络：选择本端数据库服务器所处的私有网络。若您从未新建过私有网络，选择仅有选项即可；
 - 目的端：填写固定值 `10.255.0.0/16`。若您数据库服务器本身所属网段即是 10.255.0.0/16 网段，请咨询腾讯客服或拨打 4009-100-100；
 - 下一跳类型：选择对等连接；
 - 下一跳：选择刚配置的对等连接的名称（本次举例是test）；
 - 备注：任意填写简单易记的备注信息即可。
 
 ![4](https://main.qcloudimg.com/raw/7fdf945902a09cd84a3b08c26dc5367e.png)
3. 对等网络与路由表配置完毕后，您可以登录数据库服务器，对新购的数据安全审计实例内网 IP 进行 ping 操作，查看网络是否连通。
