---
title: Cara Sizing Worker Node Redhat Openshift VM dan Baremetal
# date: 2017-09-12 13:50:39 +0000
categories:
- blog
tags:
- Openshift
layout: single

header:
  image: "uploads/3445fcd8e6b442f9a17fd5c79590ddb3.png"
  og_image: "uploads/3445fcd8e6b442f9a17fd5c79590ddb3.png"
  # caption: 'Photo Credit: Headspin.io'
excerpt: Kali ini saya akan sharing bagaimana caranya melakukan sizing worker node Redhat Openshift VM dan Baremetal, serta simulasi perhitungannya.

---

Hallo gimana kabarnya, semoga sehat selalu ya!,

Kali ini saya akan sharing gimana caranya untuk melakukan sizing Worker Node Redhat Openshift baik yang berbasis VM maupun yang berbasis baremetal.

Saya mengasumsikan temen-temen sudah mengetahui apa itu Redhat Openshift dan komponen didalamnya, mungkin saya sedikit mention tentang komponen apa aja sih didalam Redhat Openshift itu, yaitu:

**1. Worker Node**

- A Worker Node, also known as a Minion or a Compute Node, is responsible for running the actual containerized applications. These nodes host the pods (the smallest deployable units in Kubernetes) that contain the application components.
- On a Worker Node, container runtime (such as Docker or containerd) is responsible for running containers. It communicates with the Master Node to receive instructions about which containers to run and manages the containers' lifecycle on the node.
- Worker Nodes are where the application workloads are executed, and they provide the necessary resources (CPU, memory, storage) to support these workloads.

**2. Master Node**

- The Master Node is the central control plane of the OpenShift cluster. It manages and coordinates the overall cluster operations, ensuring that the desired state of the cluster matches the actual state.
- Components like the API Server, Controller Manager, Scheduler, and etcd (a distributed key-value store for cluster configuration) run on the Master Node.
- The API Server exposes the Kubernetes API, which is used by administrators, developers, and other components to interact with the cluster. The Controller Manager and Scheduler are responsible for maintaining the desired state of the cluster and scheduling workloads, respectively.

**3. Infra Router Node**

- The Infra Router Node is specific to OpenShift and is responsible for handling external HTTP and HTTPS traffic for applications running in the cluster.
- It runs routers, which are responsible for load balancing and routing external requests to the appropriate services and pods within the OpenShift cluster.
- Infra Router Nodes enhance the capabilities of standard Kubernetes Ingress by providing additional features and configurations specific to the OpenShift platform.

Intinya adalah Worker Node adalah tempat aplikasi running (aplikasi yang kita jalankan), Master Node berfungsi memanage cluster dan Infra Router Node berfungsi menghandle external traffic dan melakukan routing applications di OpenShift cluster.

Kalau dilihat Worker Node ini menjadi node yang krusial jika sizing yang dilakukan tidak tepat, berikut saya akan sharing cara sizing worker node Redhat Openshift VM dan Baremetal.

## Sizing Worker

Worker Node di Openshift yang berbasis **VM** memiliki capacity maximum **1 worker node adalah 20 vCPU**, sedangkan worker node di Openshift yang berbasis **Baremetal** karena dia adalah hardware maka **1 worker node up to 64 CPU / Core (1-2 Socket)**.

**Berikut simulasi Openshift VM**:

Assumption aplikasi di Production kita memiliki jumlah 160 vCPU, dan kita ingin menggunakan Openshift VM maka perhitungannya adalah

```
**Hardware**

160 vCPU / 20 vCPU = 8 Worker Nodes (Hardware)

**License**

160 vCPU / 4 vCPU = 40 License Openshift VM (RHCOS)

```

Sehingga kita membutuhkan **8 Worker Nodes Openshift VM** dan **license RHCOS sebanyak 40 License**


**Berikut simulasi Openshift Baremetal**:

Assumption aplikasi di Production kita memiliki jumlah 160 vCPU, dan kita ingin menggunakan Openshift Baremetal maka perhitungannya adalah

```
**Hardware**

160 vCPU / 2 / 64 vCPU = 2 Worker Nodes Baremetal (Hardware)

* vCPU harus diubah dulu ke CPU, karena 1 CPU = 2 vCPU

**License**

License yang dibutuhkan adalah 2 Worker Nodes Baremetal (jumlah license sama dengan jumlah worker node baremetal)

```

Sehingga kita membutuhkan **2 Worker Nodes Openshift Baremetal** dan **license Openshift Baremetal sebanyak 2 license**

Lalu apakah bisa Hybrid Worker Node ada di Baremetal sedangkan Infra Router Node dan Master Node ada di Openshift VM? Jawabannya adalah bisa. Sehingga secara cost bisa lebih murah Hybrid ketimbang Full Baremetal.

## Kesimpulan

Sekarang kita sudah mengetahui bagaimana cara sizing worker node Redhat Openshift VM dan Baremetal, lalu kapan kita memilih Openshift VM atau Baremetal, semua itu tergantung dengan rencana bisnis kedepannya, kalau secara harga License VM lebih murah ketimbang License Baremetal, tetapi jika dilihat secara Hardware, baremetal akan lebih mahal dibanding VM.

Intinya adalah kalau cluster Openshift kita butuh besar, maka kamu bisa memilih Baremetal, tetapi kalau cluster openshift yang kita tidak butuh terlalu besar maka VM lebih cocok karena lebih murah ketimbang Baremetal.

Mungkin itu dulu pembahasan kali ini, Keep connected!

Sekian dan terima kasih