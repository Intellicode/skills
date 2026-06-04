# Interface Patterns

## Choose the Shell

- **Sidebar workspace**: Best for dashboards, admin panels, cloud consoles, commerce back offices, and file managers. Put global navigation in the sidebar and page-specific controls in a top command bar.
- **Inbox split pane**: Best for email, notifications, support queues, logs, and reviews. Use a list pane, reading/detail pane, and bulk actions.
- **Editor canvas**: Best for docs, design tools, CMS, workflow builders, and notebooks. Use a document title row, toolbar, canvas, comments/inspector panel, and presence.
- **Table workspace**: Best for operations, CRM, billing, users, orders, resources, and permissions. Use saved views, filters, column controls, row actions, selection, and pagination.
- **Project console**: Best for deployment, cloud, observability, and infrastructure products. Use project switcher, environment/status badges, charts/logs, resource tables, and settings tabs.

## Navigation

- Use persistent global navigation for core product areas.
- Use tabs for peer views within one resource: Overview, Activity, Settings, Members, Billing.
- Use breadcrumbs when users traverse nested resources.
- Use a project/account switcher for multi-tenant SaaS.
- Put primary creation actions near the current object: "New project", "Upload", "Create order", "Invite".

## Command Bars

Include command bars above dense content. Common controls:

- Search input with clear placeholder tied to the current object.
- Filter buttons or dropdowns for status, owner, date, region, type, and saved views.
- Sort or view toggle when there are multiple valid browsing modes.
- Bulk actions that appear when rows are selected.
- Secondary actions grouped behind a menu to avoid clutter.

## Tables and Lists

- Give every table a clear object type and realistic columns.
- Align numbers and dates for scanning.
- Use status chips with text and color; never rely on color alone.
- Keep row actions visible on hover or in a final actions column.
- Include empty, loading, and error states for data-heavy screens.
- For mobile, collapse low-priority columns into stacked metadata or a details drawer.

## Detail Panels

Use a right-side detail panel when the user needs context without leaving a list:

- Summary header with object name, status, and primary action.
- Metadata list for owner, updated date, region, plan, or permissions.
- Activity feed or comments when collaboration matters.
- Destructive actions separated visually at the bottom.

## Forms and Settings

- Group settings by user intent, not database fields.
- Use inline validation and explanatory help text only where it prevents errors.
- Keep destructive settings isolated and confirmed.
- Preserve unsaved-change state with clear save/cancel controls.
- Use progressive disclosure for advanced options.

## Collaboration

For productivity SaaS, include indicators that make the product feel real:

- Avatars or initials for presence and ownership.
- Comments, mentions, review status, or activity.
- Permission levels: Owner, Editor, Viewer, Billing admin.
- Sharing controls with invite field and access summary.
