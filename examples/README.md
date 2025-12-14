# Table-Remodeler Examples

This directory contains Jupyter notebooks demonstrating how to use the table-remodeler package for various data transformation and analysis tasks.

## Running the Examples

### Prerequisites

Install table-remodeler with Jupyter support:

```bash
pip install table-remodeler
pip install jupyter notebook
```

Or if developing locally from this repository:

```bash
pip install -e ".[dev]"
```

### Launching Notebooks

From the repository root:

```bash
jupyter notebook examples/
```

Or in VS Code, simply open the `.ipynb` files directly.

## Available Examples

### 1. [run_remodel_backup.ipynb](run_remodel_backup.ipynb)
Demonstrates creating backups of tabular data files before performing remodeling operations. Shows how to:
- Create named backups
- Exclude specific directories
- Control which file types to backup

### 2. [run_remodel.ipynb](run_remodel.ipynb)
Demonstrates executing remodeling operations on tabular data using JSON configuration files. Shows how to:
- Apply transformation operations to data files
- Use remodeling operation specifications
- Control output and logging

### 3. [run_remodel_restore.ipynb](run_remodel_restore.ipynb)
Demonstrates restoring files from previously created backups. Shows how to:
- Restore from named backups
- Revert changes made by remodeling operations

## Data Requirements

The notebooks use test data from the repository's `tests/data/` directory. The test data is automatically extracted from `test_root.zip` when you run the notebooks, so no additional setup is required.

## Workflow Sequence

For a complete remodeling workflow, run the notebooks in this order:

1. **run_remodel_backup.ipynb** - Create a backup before making changes
2. **run_remodel.ipynb** - Apply remodeling operations to your data
3. **run_remodel_restore.ipynb** - (Optional) Restore original files if needed

## Contributing

If you create new example notebooks, please:
1. Add clear markdown documentation in cells
2. Include expected outputs
3. Use test data from `tests/data/` when possible
4. Test that the notebook runs end-to-end
5. Update this README with a brief description
