---
name: optimus-ui
description: Local, offline copy of the official Optimus UI (@openng/optimus-ui) documentation — usage examples, full API (props, events, templates), pass-through options, CSS classes and design tokens for all 80+ Angular components, plus the installation, configuration, theming (styled/unstyled), icons, Tailwind, pass-through, accessibility and PrimeNG-migration guides. Use this skill whenever writing, reviewing, debugging or answering questions about Angular code that uses Optimus UI — any `p-*` element or `p*` directive (p-button, p-table, p-select, p-dialog, pTooltip, ...), imports from `@openng/optimus-ui` or `@openng/optimus-ui-themes`, theming/design tokens, or migrating from PrimeNG — and prefer it over fetching optimus.openng.org pages.
license: MIT
metadata:
  author: OpenNG (Optimus UI)
  version: "2.0.2"
  source: https://optimus.openng.org
---

# Optimus UI docs (local copy)

Optimus UI is a community-maintained, MIT-licensed continuation of PrimeNG: 80+ accessible Angular components, targeting Angular v21+. This skill bundles the documentation published at <https://optimus.openng.org/llms/llms.txt> (generated from Optimus UI v2.0.2), so you can read it from disk instead of fetching `https://optimus.openng.org/llms/components/<name>.md` each time.

All paths below are relative to this skill's directory (the folder containing this SKILL.md).

## How to use the docs

1. Find the file in the index below. The file name is the component's docs slug (`select`, `datepicker`, `inputotp`, `galleria`, `scroller`, ...), which is not always the selector name.
2. Read only the part you need. Component files are 10–60 KB, so list the headings first and then read the matching line range, for example `grep -n '^##' references/components/table.md`.
3. When an exact API detail matters (input name, event payload, template context, token name), copy it from the docs instead of relying on memory of PrimeNG. Optimus UI is API-compatible with PrimeNG v21 in most places, but names, packages and defaults can differ.

To search everything at once, grep the folder, for example `grep -rn "appendTo" references/components/`.

### Layout of a component file

- `# Angular <Name> Component` followed by a one-line summary.
- One `##` section per demo (Basic, Template, Sizes, Disabled, ...). Each has a short explanation and a full standalone Angular component in a `typescript` block showing the correct imports.
- `## Accessibility`: screen-reader and keyboard support.
- `## <Name>` with `### Props`, `### Emits`, `### Templates` (and sometimes `### Methods`): the API tables. This is the authoritative list of inputs and outputs.
- `## Pass Through Options`: the `pt` keys for styling internal elements.
- `## Theming`, with `### CSS Classes` and `### Design Tokens`.

## Conventions that hold across the library

Check the guides when in doubt; these are here so simple tasks don't need a lookup:

- Packages: `@openng/optimus-ui` (one secondary entry point per component, such as `@openng/optimus-ui/button`) and `@openng/optimus-ui-themes` (theme presets).
- Components are imported per entry point (`import { ButtonModule } from '@openng/optimus-ui/button'`) into standalone components. The docs examples show the exact symbol to import, so copy it from there.
- App-wide setup (theme preset, ripple, z-index, locale and so on) goes through `provideOptimus({...})` from `@openng/optimus-ui/config`; see `references/guides/configuration.md`. New projects can use `ng add @openng/optimus-ui`. Existing PrimeNG apps use the `migrate-from-primeng` schematic instead (see `references/guides/installation.md` and `references/guides/faq.md`).
- Selectors use the `p-` prefix (`<p-button>`, `<p-table>`) and directives the `p` prefix (`pButton`, `pTooltip`, `pInputText`).

## Keeping the docs up to date

These docs are a snapshot of v2.0.2. If the project uses a newer Optimus UI release, or the docs contradict the installed package, offer to update it by running `npx skills update optimus-ui`, or `npx skills add https://optimus.openng.org` (add `-g` for a user-level install) if it was installed another way. Any single page can also be fetched live from `https://optimus.openng.org/llms/components/<name>.md` or `https://optimus.openng.org/llms/pages/<name>.md`.

## Index

### Guides (`references/guides/`)

- `references/guides/accessibility.md` — **Accessibility**: Optimus UI has WCAG 2.1 AA level compliance.
- `references/guides/animations.md` — **Animations**: Built-in CSS animations for Optimus UI components.
- `references/guides/configuration.md` — **Configuration**: Application wide configuration for Optimus UI.
- `references/guides/contribution.md` — **Contribution Guide**: How to contribute to Optimus UI.
- `references/guides/customicons.md` — **Custom Icons**: Use custom icons with Optimus UI components.
- `references/guides/faq.md` — **FAQ**: Licensing, migration from PrimeNG, the ecosystem, and how support works.
- `references/guides/icons.md` — **Icons**: OpenNG Icons is the default icon library of Optimus UI with over 250 open source icons.
- `references/guides/installation.md` — **Installation**: Setting up Optimus UI in an Angular CLI project.
- `references/guides/llms.md` — **LLMs.txt**: LLM-optimized documentation endpoints for Optimus UI components.
- `references/guides/passthrough.md` — **Pass Through**: Pass Through Props allow direct access to the underlying elements for complete customization.
- `references/guides/philosophy.md` — **Philosophy**: Why Optimus UI exists, what it commits to, and where it stops.
- `references/guides/primeflex.md` — **PrimeFlex**: Moving from PrimeFlex to Tailwind CSS.
- `references/guides/rtl.md` — **RTL**: Right-to-left support for Optimus UI components.
- `references/guides/styled.md` — **Styled Mode**: Choose from a variety of pre-styled themes or develop your own.
- `references/guides/tailwind.md` — **Tailwind CSS**: Integration between Optimus UI and Tailwind CSS.
- `references/guides/unstyled.md` — **Unstyled Mode**: Theming Optimus UI with alternative styling approaches.

### Components (`references/components/`)

- `references/components/accordion.md` — **Accordion**: Accordion groups a collection of contents in tabs.
- `references/components/animateonscroll.md` — **Animate On Scroll**: AnimateOnScroll is used to apply animations to elements when entering or leaving the viewport during scrolling.
- `references/components/autocomplete.md` — **AutoComplete**: AutoComplete is an input component that provides real-time suggestions when being typed.
- `references/components/autofocus.md` — **AutoFocus**: AutoFocus manages focus on focusable element on load.
- `references/components/avatar.md` — **Avatar**: Avatar represents people using icons, labels and images.
- `references/components/badge.md` — **Badge**: Badge is a small status indicator for another element.
- `references/components/blockui.md` — **BlockUI**: BlockUI can either block other components or the whole page.
- `references/components/breadcrumb.md` — **Breadcrumb**: Breadcrumb provides contextual information about page hierarchy.
- `references/components/button.md` — **Button**: Button is an extension to standard button element with icons and theming.
- `references/components/card.md` — **Card**: Card is a flexible container component.
- `references/components/carousel.md` — **Carousel**: Carousel is a content slider featuring various customization options.
- `references/components/cascadeselect.md` — **CascadeSelect**: CascadeSelect displays a nested structure of options.
- `references/components/chart.md` — **Chart**: Chart components are based on Charts.js 3.3.2+, an open source HTML5 based charting library.
- `references/components/checkbox.md` — **Checkbox**: Checkbox is an extension to standard checkbox element with theming.
- `references/components/chip.md` — **Chip**: Chip represents entities using icons, labels and images.
- `references/components/colorpicker.md` — **ColorPicker**: ColorPicker is an input component to select a color.
- `references/components/confirmdialog.md` — **ConfirmDialog**: ConfirmDialog is backed by a service utilizing Observables to display confirmation windows easily that can be shared by multiple actions on the same component.
- `references/components/confirmpopup.md` — **ConfirmPopup**: ConfirmPopup displays a confirmation overlay displayed relatively to its target.
- `references/components/contextmenu.md` — **ContextMenu**: ContextMenu displays an overlay menu on right click of its target.
- `references/components/dataview.md` — **DataView**: DataView displays data in grid grid-cols-12 gap-4 or list layout with pagination and sorting features.
- `references/components/datepicker.md` — **DatePicker**: DatePicker is an input component to select a date.
- `references/components/dialog.md` — **Dialog**: Dialog is a container to display content in an overlay window.
- `references/components/divider.md` — **Divider**: Divider is used to separate contents.
- `references/components/dock.md` — **Dock**: Dock is a navigation component consisting of menuitems.
- `references/components/dragdrop.md` — **Drag and Drop**: pDraggable and pDroppable directives apply drag-drop behaviors to any element.
- `references/components/drawer.md` — **Drawer**: Drawer is a container component displayed as an overlay.
- `references/components/dynamicdialog.md` — **Dynamic Dialog**: Dialogs can be created dynamically with any component as the content using a DialogService.
- `references/components/editor.md` — **Editor**: Editor is rich text editor component based on Quill.
- `references/components/fieldset.md` — **Fieldset**: Fieldset is a grouping component with a content toggle feature.
- `references/components/fileupload.md` — **FileUpload**: FileUpload is an advanced uploader with dragdrop support, multi file uploads, auto uploading, progress tracking and validations.
- `references/components/floatlabel.md` — **Float Label**: FloatLabel appears on top of the input field when focused.
- `references/components/fluid.md` — **Fluid**: Fluid is a layout component to make descendant components span full width of their container.
- `references/components/focustrap.md` — **Focus Trap**: Focus Trap keeps focus within a certain DOM element while tabbing.
- `references/components/galleria.md` — **Gallery**: Galleria is an advanced content gallery component.
- `references/components/iconfield.md` — **IconField**: IconField wraps an input and an icon.
- `references/components/iftalabel.md` — **Ifta Label**: IftaLabel is used to create infield top aligned labels.
- `references/components/imagecompare.md` — **ImageCompare**: Compare two images side by side with a slider.
- `references/components/inplace.md` — **Inplace**: Inplace provides an easy to do editing and display at the same time where clicking the output displays the actual content.
- `references/components/inputgroup.md` — **InputGroup**: Text, icon, buttons and other content can be grouped next to an input.
- `references/components/inputmask.md` — **InputMask**: InputMask component is used to enter input in a certain format such as numeric, date, currency and phone.
- `references/components/inputnumber.md` — **InputNumber**: InputNumber is an input component to provide numerical input.
- `references/components/inputotp.md` — **Otp Input**: Input Otp is used to enter one time passwords.
- `references/components/inputtext.md` — **InputText**: InputText is an extension to standard input element with theming and keyfiltering.
- `references/components/keyfilter.md` — **KeyFilter**: KeyFilter is a directive to restrict individual key strokes. In order to restrict the whole input, use InputNumber or InputMask instead.
- `references/components/knob.md` — **Knob**: Knob is a form component to define number inputs with a dial.
- `references/components/listbox.md` — **Listbox**: Listbox is used to select one or more values from a list of items.
- `references/components/megamenu.md` — **MegaMenu**: MegaMenu is navigation component that displays submenus together.
- `references/components/menu.md` — **Menu**: Menu is a navigation / command component that supports dynamic and static positioning.
- `references/components/menubar.md` — **Menubar**: Menubar is a horizontal menu component.
- `references/components/message.md` — **Message**: Message component is used to display inline messages.
- `references/components/metergroup.md` — **MeterGroup**: MeterGroup displays scalar measurements within a known range.
- `references/components/multiselect.md` — **MultiSelect**: MultiSelect is used to select multiple items from a collection.
- `references/components/orderlist.md` — **OrderList**: OrderList is used to sort a collection.
- `references/components/organizationchart.md` — **Organization Chart**: OrganizationChart visualizes hierarchical organization data.
- `references/components/overlay.md` — **Overlay API**: This API allows overlay components to be controlled from the Optimus UI. In this way, all overlay components in the application can have the same behavior.
- `references/components/paginator.md` — **Paginator**: Paginator displays data in paged format and provides navigation between pages.
- `references/components/panel.md` — **Panel**: Panel is a container component with an optional content toggle feature.
- `references/components/panelmenu.md` — **PanelMenu**: PanelMenu is a hybrid of Accordion and Tree components.
- `references/components/password.md` — **Password**: Password displays strength indicator for password fields.
- `references/components/picklist.md` — **PickList**: PickList is used to reorder items between different lists.
- `references/components/popover.md` — **Popover**: Popover is a container component that can overlay other components on page.
- `references/components/progressbar.md` — **ProgressBar**: ProgressBar is a process status indicator.
- `references/components/progressspinner.md` — **ProgressSpinner**: ProgressSpinner is a process status indicator.
- `references/components/radiobutton.md` — **RadioButton**: RadioButton is an extension to standard radio button element with theming.
- `references/components/rating.md` — **Rating**: Rating component is a star based selection input.
- `references/components/ripple.md` — **Ripple**: Ripple directive adds ripple effect to the host element.
- `references/components/scroller.md` — **Virtual Scroller**: VirtualScroller is a performance-approach to handle huge data efficiently.
- `references/components/scrollpanel.md` — **Scroll Panel**: ScrollPanel is a cross browser, lightweight and skinnable alternative to native browser scrollbar.
- `references/components/scrolltop.md` — **Scroll Top**: ScrollTop gets displayed after a certain scroll position and used to navigates to the top of the page quickly.
- `references/components/select.md` — **Select**: Select is used to choose an item from a collection of options.
- `references/components/selectbutton.md` — **SelectButton**: SelectButton is used to choose single or multiple items from a list using buttons.
- `references/components/skeleton.md` — **Skeleton**: Skeleton is a placeholder to display instead of the actual content.
- `references/components/slider.md` — **Slider**: Slider is a component to provide input with a drag handle.
- `references/components/speeddial.md` — **Speed Dial**: SpeedDial is a floating button with a popup menu.
- `references/components/splitbutton.md` — **SplitButton**: SplitButton groups a set of commands in an overlay with a default action item.
- `references/components/splitter.md` — **Splitter**: Splitter is utilized to separate and resize panels.
- `references/components/stepper.md` — **Stepper**: The Stepper component displays a wizard-like workflow by guiding users through the multi-step progression.
- `references/components/styleclass.md` — **StyleClass**: StyleClass manages css classes declaratively to during enter/leave animations or just to toggle classes on an element.
- `references/components/table.md` — **Table**: Table displays data in tabular format.
- `references/components/tabs.md` — **Tabs**: Tabs is a container component to group content with tabs.
- `references/components/tag.md` — **Tag**: Tag component is used to categorize content.
- `references/components/terminal.md` — **Terminal**: -
- `references/components/textarea.md` — **Textarea**: Textarea adds styling and autoResize functionality to standard textarea element.
- `references/components/tieredmenu.md` — **TieredMenu**: TieredMenu displays submenus in nested overlays.
- `references/components/timeline.md` — **Timeline**: Timeline visualizes a series of chained events.
- `references/components/toast.md` — **Toast**: Toast is used to display messages in an overlay.
- `references/components/togglebutton.md` — **ToggleButton**: ToggleButton is used to select a boolean value using a button.
- `references/components/toggleswitch.md` — **ToggleSwitch**: ToggleSwitch is used to select a boolean value.
- `references/components/toolbar.md` — **Toolbar**: Toolbar is a grouping component for buttons and other content.
- `references/components/tooltip.md` — **Tooltip**: Tooltip directive provides advisory information for a component. Tooltip is integrated within various Optimus UI components.
- `references/components/tree.md` — **Tree**: Tree is used to display hierarchical data.
- `references/components/treeselect.md` — **TreeSelect**: TreeSelect is a form component to choose from hierarchical data.
- `references/components/treetable.md` — **TreeTable**: TreeTable is used to display hierarchical data in tabular format.
