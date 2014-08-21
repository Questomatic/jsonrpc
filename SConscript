# vim:ai:et:ff=unix:fileencoding=utf-8:sw=4:syntax=python:ts=4:

import os

env = Environment(
    ENV=os.environ,
    tools=['default', 'mb_install'],
    toolpath=['#/../mw-scons-tools'])

env.MBAddStandardCompilerFlags()

env.MBAddIncludePaths([
    Dir('src/main/include/'),
    Dir('src/main/')])

env.MBDependsOnJsonCpp()

libjsonrpc = env.MBSharedLibrary(
    'jsonrpc', [Glob('src/main/cpp/*.cpp')])
env.Clean(libjsonrpc, '#/obj')

env.MBInstallLib(libjsonrpc, 'jsonrpc')
env.MBInstallHeaders(env.MBGlob('#/src/main/include/jsonrpc/*'), 'jsonrpc')

env.MBCreateInstallTarget()
