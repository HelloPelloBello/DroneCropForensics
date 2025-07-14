\#  DroneCropForensics - Incident Timeline



| Time (UTC)       | Event                                                                 |

|------------------|------------------------------------------------------------------------|

| 2025-07-12 04:45 | Attacker accessed S3 bucket: dronecrop-images via `GetObject` API     |

| 2025-07-12 04:50 | Used AWS API: `DescribeInstances` — recon on EC2 setup                 |

| 2025-07-12 05:02 | Called `StartInstances` — powered up EC2 instance                     |

| 2025-07-12 05:07 | SSH login success from IP: `91.203.119.5`                             |

| 2025-07-12 05:08 | Crypto miner downloaded \& executed                                    |

| 2025-07-12 05:11 | Drone API file `upload.php` deleted (breaking image upload system)    |

| 2025-07-12 05:13 | Drone tried uploading image → `404 Not Found` API error               |



