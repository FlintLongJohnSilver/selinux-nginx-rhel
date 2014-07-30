###############################################################################
# SELinux Reference Policy Module for Nginx on RHEL/CentOS
# 
# Copyright 2014 by J. Armando Uch <jahrmando@gmail.com>
# Copyright 2013 by Joe Johnston <joe@simple10.com>
# Copyright 2009 by Stuart Cianos <scianos@alphavida.com>
# 
# Licensed under GNU General Public License 3.0 or later. 
# Some rights reserved. See COPYING, AUTHORS.
# 
# @license GPL-3.0+ <http://spdx.org/licenses/GPL-3.0+>
###############################################################################

# From /usr/src/selinux-policy-src/doc/Makefile.example

AWK ?= gawk

NAME ?= $(shell $(AWK) -F= '/^SELINUXTYPE/{ print $$2 }' /etc/selinux/config)
SHAREDIR ?= /usr/share/selinux

HEADERDIR := $(SHAREDIR)/devel/include
include $(HEADERDIR)/Makefile