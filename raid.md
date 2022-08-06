

`Redundant Array of Independent Disks`

RAID is a storage technology that helps against data lose & performance or both at the same time depending on the chosen `RAID Configuration`. 
RAID makes physical storage devices look like a single logical device by using whats called a `RAID Controler`.
The data redundancy feature is based on parity calculations, which allows the user to access the data even if the disk containing is has failed and can also populate a new disk with the extracted data.

# Capabilities

- Stripping
- Mirroring
- Parity Check

# Configurations

## RAID 0

- Stripping only
- The best performance
- 100% Storage Capacity

## RAID 1

- Mirroring only
- 50% Storage Capacity
- Multiple Disk Controllers to reduce load since data is being read two times

## RAID 5

## RAID 10

- Stripping with RAID 0 & Mirroring the RAID 0 instances with RAID 1
