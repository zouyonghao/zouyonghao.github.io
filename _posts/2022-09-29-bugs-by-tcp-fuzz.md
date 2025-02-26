---
title: Bugs found by TCP-Fuzz (opensource projects only, update: 2025)
layout: post
---

Here I list some of bugs found by TCP-Fuzz for opensource projects.

* mTCP
    * [Remove mtcp listener before it is freed.](https://github.com/mtcp-stack/mtcp/pull/320)
    * [Validate ip length before using tcp header.](https://github.com/mtcp-stack/mtcp/pull/319)
    * [Accept the packet with seq smaller than the last received packet](https://github.com/mtcp-stack/mtcp/pull/316)
    * [Fix out of bound read](https://github.com/mtcp-stack/mtcp/pull/315)
    * [Check first ack packet to update its timestamp value](https://github.com/mtcp-stack/mtcp/pull/314)
    * [Accept packets without timestamp option](https://github.com/mtcp-stack/mtcp/pull/313)
    * [Fix 0 mss if we do not receive mss before](https://github.com/mtcp-stack/mtcp/pull/312)
    * [Fix NULL pointer if we read before receiving any packet with data](https://github.com/mtcp-stack/mtcp/pull/311)

* F-Stack
    * [Duplicated packets cause read error?](https://github.com/F-Stack/f-stack/issues/556)
    * [Some issues of current version FreeBSD](https://github.com/F-Stack/f-stack/issues/555)

* FreeBSD
    * [RFC 5961 is not implemented completely](https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=250357)
    * [connections should be closed if a same packet without FIN is received after FIN received](https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=250360)
    * [data in syn_ack should be ignored](https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=250363)
    * [The ioctl of socket fd should return -1 after listen to avoid misusing.](https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=250366)
    * [Should we reject the packet with timestamp if no timestamp in SYN and SYN_ACK?](https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=250499)
    * [Should we reject packets with the nonmonotonic timestamp?](https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=252263)

* Linux
    * [RFC 7323 violation](https://lore.kernel.org/netdev/20250224110654.707639-1-edumazet@google.com/)