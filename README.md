# WheelOS Control

Independent `wheelos_control` Bzlmod module. Sources and Proto imports retain
their `modules/control/...` paths. Core, Common and messages supply shared
runtime contracts; the package does not depend on the Apollo product.

In the mapped-user managed development container, from `/apollo`:

```bash
python3 scripts/bzlmod.py dev build --config=cpu --config=opt @wheelos_control//modules/control:libcontrol_component.so
python3 scripts/bzlmod.py dev test --config=cpu --config=opt @wheelos_control//modules/control/common:motion_execution_manager_test
```

The Planning/Control joint regression is owned by the product:
`//tools/control/tests:motion_chain_contract_test`. Module tests include a
frozen vehicle configuration; live configuration still belongs to the
selected deployment. See [component documentation](modules/control/README.md).

Standalone and Apollo-root SDK installs apply the
`third_party/rules_pkg/execroot_runfiles.patch` override. It keeps externally
owned shared-library runfiles relative to the execution root. Other consuming
roots must carry the same override; dependency-module overrides are ignored.

Like `transform`, this ignored checkout must accompany the product changes.
Its Git source is registered in `wheelos.repos`; no Bzlmod registry release
has been published. Local overrides are not evidence of registry consumption.
