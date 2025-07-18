project('pci-ids', 'rust')

parser_exe = executable(
  'parser',
  'build.rs',
  dependencies: [
    dependency('nom-7-rs', native: true),
    dependency('phf_codegen-0.11-rs', native: true),
    dependency('quote-1-rs', native: true),
    dependency('proc-macro2-1-rs', native: true),
  ],
  native: true
)

generated = custom_target(
  'pci_ids.cg.rs',
  input: 'pciids/pci.ids',
  output: 'pci_ids.cg.rs',
  command: [parser_exe, '@INPUT@', '@OUTDIR@']
)

pci_ids_lib = static_library(
  'pci_ids',
  structured_sources([
    'src/lib.rs',
    generated
  ]),
  dependencies: [
    dependency('phf-0.11-rs')
  ]
)

meson.override_dependency(
  'pci-ids-0.2-rs',
  declare_dependency(
    link_with: [pci_ids_lib]
  )
)
