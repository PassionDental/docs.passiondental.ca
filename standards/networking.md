# Passion Dental Subnets

At Passion, all address space is predetermined.

## Subnet Calculator

Use this subnet calculator to determine the subnet for each location.

https://subnets.passiondental.ca/

**Note:** the /28 data centre subnets are not applicable right now

## AWS Subnet Space

We use 10.255.0.0/16 as the VPC address space
### ca-central-1a

We use the following in the zone a:

- Public Subnet: 10.255.0.0/24
- Private Subnet: 10.255.100.0/23
### ca-central-1b

We use the following in the zone b:

- Public Subnet: 10.255.1.0/24
- Private Subnet: 10.255.200.0/23

## Data Centre Subnet Space

10.0.0.0-10.0.62.255


Currently in use:
10.0.1.0/24 - Client VPN

## Clinic Subnet Space

10.100.0.0-10.111.255.255 (I'd rather allocate 10.100.0.0/12, which is really 10.96.0.0/12)
10.240.0.0/16

10.240.100.0/23 = Client VPN zone A
10.240.102.0/23 = Client VPN zone b

## Azure Subnet Space

10.241.0.0/16 = Azure