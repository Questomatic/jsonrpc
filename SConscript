# vim:ai:et:ff=unix:fileencoding=utf-8:sw=4:syntax=python:ts=4:
# jsonrpc/SConscript
#
# jsonrpc - JSON-RPC 2.0 for QT
# Copyright © 2012 Matthew W. Samsonoff <matthew.samsonoff@makerbot.com>
#
# This program is free software: you can redistribute it and/or modify it under
# the terms of the GNU Affero General Public License as published by the Free
# Software Foundation, either version 3 of the License, or (at your option) any
# later version.
#
# This program is distributed in the hope that it will be useful, but WITHOUT
# ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS
# FOR A PARTICULAR PURPOSE. See the GNU Affero General Public License for more
# details.
#
# You should have received a copy of the GNU Affero General Public License
# along with this program. If not, see <http://www.gnu.org/licenses/>.

import os.path

env = Environment()

if 'QTDIR' not in env:
    moc = env.WhereIs('moc-qt4') or env.WhereIs('moc4') or env.WhereIs('moc')
    if moc:
        env['QTDIR'] = os.path.dirname(os.path.dirname(moc))

env.Tool('qt4', toolpath=[Dir('#/src/main/scons/')])
env.EnableQt4Modules(['QtCore', 'QtTest'])
env.Append(CCFLAGS='-pedantic')
env.Append(CCFLAGS='-Wall')
env.Append(CCFLAGS='-Wextra')
env.Append(CCFLAGS='-Wno-variadic-macros')
env.Append(CCFLAGS='-Wno-long-long')
env.Append(CCFLAGS='-Werror')

cppenv = env.Clone()
cppenv.Append(CPPPATH=Dir('#/obj/src/main/cpp/'))
libjsonrpc = cppenv.Library('jsonrpc', Glob('#/obj/src/main/cpp/jsonrpc/*.cpp'))

testenv = cppenv.Clone()
testenv.AlwaysBuild('check')
testenv.Append(LIBS=libjsonrpc)
for node in Glob('#/obj/src/test/cpp/test-*.cpp'):
    root, ext = os.path.splitext(os.path.basename(node.abspath))
    test = testenv.Program(root, [node])
    alias = testenv.Alias('check', [test], test[0].abspath)
    testenv.AlwaysBuild(alias)
