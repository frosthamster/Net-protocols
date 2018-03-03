# Шаг 7

`Анисимов Данил - ФТ-201`

```
Router>en
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.

Router(config)#int se 2/0
Router(config-if)#ip addr 10.3.3.2 255.255.255.0
Router(config-if)#no shut
Router(config-if)#ex

Router(config)#int loo 0

Router(config-if)#
%LINK-5-CHANGED: Interface Loopback0, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Loopback0, changed state to up

Router(config-if)#ip addr 172.20.0.1 255.255.255.0
Router(config-if)#int loo 1

Router(config-if)#
%LINK-5-CHANGED: Interface Loopback1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Loopback1, changed state to up

Router(config-if)#ip addr 172.20.1.1 255.255.255.0
Router(config-if)#int loo 2

Router(config-if)#
%LINK-5-CHANGED: Interface Loopback2, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Loopback2, changed state to up

Router(config-if)#ip addr 172.20.2.1 255.255.255.0
Router(config-if)#ex

Router(config)#rout rip
Router(config-router)#vers 2
Router(config-router)#no auto-
Router(config-router)#no auto-summary 
Router(config-router)#net
Router(config-router)#network 10.0.0.0
Router(config-router)#net 172.20.0.0
Router(config-router)#ex


R2AR0(config)#router rip
R2AR0(config-router)#version 2
R2AR0(config-router)#no auto-summary 
R2AR0(config-router)#network 10.0.0.0

R2AR0(config)#router ospf 1
R2AR0(config-router)#redistribute rip subnets 
R2AR0(config-router)#ex
```

```
R1AR0>en
R1AR0#sh ip ro
Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

     10.0.0.0/8 is variably subnetted, 7 subnets, 2 masks
C       10.1.1.0/24 is directly connected, Serial2/0
C       10.2.2.0/24 is directly connected, FastEthernet0/0
O E2    10.3.3.0/24 [110/20] via 10.2.2.2, 00:05:51, FastEthernet0/0
O       10.10.0.1/32 [110/2] via 10.2.2.2, 01:18:18, FastEthernet0/0
O       10.10.1.1/32 [110/2] via 10.2.2.2, 01:18:18, FastEthernet0/0
O       10.10.2.1/32 [110/2] via 10.2.2.2, 01:18:18, FastEthernet0/0
O       10.10.3.1/32 [110/2] via 10.2.2.2, 01:18:18, FastEthernet0/0
     172.20.0.0/24 is subnetted, 3 subnets
O E2    172.20.0.0 [110/20] via 10.2.2.2, 00:05:51, FastEthernet0/0
O E2    172.20.1.0 [110/20] via 10.2.2.2, 00:05:51, FastEthernet0/0
O E2    172.20.2.0 [110/20] via 10.2.2.2, 00:05:51, FastEthernet0/0
O IA 192.168.1.0/24 [110/128] via 10.1.1.2, 01:18:43, Serial2/0
O IA 192.168.2.0/24 [110/192] via 10.1.1.2, 01:18:33, Serial2/0


R1AR0#show ip ospf database external

            OSPF Router with ID (1.1.1.1) (Process ID 1)

                Type-5 AS External Link States

  Routing Bit Set on this LSA
  LS age: 1651
  Options: (No TOS-capability, DC)
  LS Type: AS External Link
  Link State ID: 10.3.3.0 (External Network Number )
  Advertising Router: 2.2.2.2
  LS Seq Number: 80000001
  Checksum: 0xc5e2
  Length: 36
  Network Mask: /24
        Metric Type: 2 (Larger than any link state path)
        TOS: 0
        Metric: 20
        Forward Address: 0.0.0.0
        External Route Tag: 0

  Routing Bit Set on this LSA
  LS age: 448
  Options: (No TOS-capability, DC)
  LS Type: AS External Link
  Link State ID: 172.20.0.0 (External Network Number )
  Advertising Router: 2.2.2.2
  LS Seq Number: 80000001
  Checksum: 0xd81f
  Length: 36
  Network Mask: /24
        Metric Type: 2 (Larger than any link state path)
        TOS: 0
        Metric: 20
        Forward Address: 0.0.0.0
        External Route Tag: 0

  Routing Bit Set on this LSA
  LS age: 448
  Options: (No TOS-capability, DC)
  LS Type: AS External Link
  Link State ID: 172.20.1.0 (External Network Number )
  Advertising Router: 2.2.2.2
  LS Seq Number: 80000001
  Checksum: 0xcd29
  Length: 36
  Network Mask: /24
        Metric Type: 2 (Larger than any link state path)
        TOS: 0
        Metric: 20
        Forward Address: 0.0.0.0
        External Route Tag: 0

  Routing Bit Set on this LSA
  LS age: 448
  Options: (No TOS-capability, DC)
  LS Type: AS External Link
  Link State ID: 172.20.2.0 (External Network Number )
  Advertising Router: 2.2.2.2
  LS Seq Number: 80000001
  Checksum: 0xc233
  Length: 36
  Network Mask: /24
        Metric Type: 2 (Larger than any link state path)
        TOS: 0
        Metric: 20
        Forward Address: 0.0.0.0
        External Route Tag: 0
```


1. В таблице маршрутизации появились записи с кодом «O E2».Что они означают? 

ospf external type 2 - учитывается только метрика перехода между AS

2. Объяснить смысл данных выводимых командой show ip ospf database external. 

Выводится информация о сетях, использующих другие протоколы маршрутизации

3. Кто и каким образом генерирует External LSA? Какую информацию содержат External LSA? 

Генерируются пограничным роутером AS, содержат информацию о внешних сетях


# Шаг 8
Выполнить на всех роутерах 1 области

```
ABR(config)#router ospf 1
ABR(config-router)#area 1 stub
```

1. Что такое тупиковая область? Для чего нужна? 
Такая зона не принимает внешние маршруты. Это позволяет сократить таблицу маршрутизации и снизить объём служебного трафика.

2. Как отразилось на таблице маршрутизации и содержимом топологической базы маршрутизаторов ABR и R1AR1 то, что область стала тупиковой? 
На роутере R1AR1 внешние маршруты заменились на дефолтный (*)

3. Предположим, что из области Area 1 понадобилось передать в OSPF какой-то внешний маршрут, например, пробросить статический маршрут до провайдера и т.д. В топологии в Area 1 есть роутер ASBR, на котором настроено несколько статических маршрутов. Удаётся ли передать эти маршруты в OSPF? Почему?
Нет, т.к. stub области запрещают хождение external LSA. Для решения этой проблемы существует NSSA области



ABR(config)#router ospf 1

ABR(config-router)#no area 1 stub 
ABR(config-router)#
02:03:18: %OSPF-5-ADJCHG: Process 1, Nbr 3.3.3.3 on Serial3/0 from FULL to DOWN, Neighbor Down: Adjacency forced to reset

02:03:18: %OSPF-5-ADJCHG: Process 1, Nbr 3.3.3.3 on Serial3/0 from FULL to DOWN, Neighbor Down: Interface down or detached
a
ABR(config-router)#area 1 nssa 
ABR(config-router)#default-information originate 

ASBR(config-router)#redistribute static subnets