# Maintainer: 4javier <4javiereg4 at gmail dot com>
# Contributor: American_Jesus
pkgname=notify-osd-customizable-gtk2
_realname=notify-osd
pkgver=0.9.30
pkgrel=4
pkgdesc="daemon that displays passive pop-up notifications, with leolik patch added"
arch=(i686 x86_64)
url="https://launchpad.net/notify-osd"
license=('GPL')
groups=()
depends=('libnotify>=0.7.0' 'dbus-glib>=0.76' 'libwnck' 'gconf>=2.28')
optdepends=('notifyconf: gui to customize notifies appearence')
makedepends=('pkgconfig' 'libnotify' 'gnome-common')
provides=('notification-daemon' 'notify-osd')
conflicts=('notification-daemon' 'notify-osd')
install=$pkgname.install
source=(https://launchpad.net/~leolik/+archive/leolik/+files/${_realname}_${pkgver}-0ubuntu4-leolik~ppa1-1.tar.gz notify-osd)
md5sums=('21f8b0fe77e8185415093c1c716bd348' '1b1c942c8caebbdaad8402dbd0a8160a')


build() {
  cd "$srcdir/$_realname-$pkgver"
  #sed -i 's,/usr/lib/notify-osd/,@LIBEXECDIR@/,' data/org.freedesktop.Notifications.service.in
  sh configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var --libexecdir=/usr/lib/$pkgname \
              --disable-static
  # Disable building tests
  sed -i '/SUBDIRS/ s/tests //' Makefile.in

  make || return 1
 }

package() {
	cd "$srcdir/$_realname-$pkgver"
	make DESTDIR="$pkgdir/" install
	install -D -m644 ${srcdir}/notify-osd ${pkgdir}/etc/skel/.notify-osd
 }
