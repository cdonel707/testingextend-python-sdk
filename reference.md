# Reference
## WorkflowEndpoints
<details><summary><code>client.workflow_endpoints.<a href="src/fernstarterpack/workflow_endpoints/client.py">list_workflow_runs</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List runs of a Workflow. Workflows are sequences of steps that process files and data in a specific order to achieve a desired outcome. A WorkflowRun represents a single execution of a workflow against a file.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.workflow_endpoints.list_workflow_runs()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**status:** `typing.Optional[WorkflowStatus]` 

Filters workflow runs by their status. If not provided, no filter is applied.

 The status of a workflow run:
 * `"PENDING"` - The workflow run has not started yet
 * `"PROCESSING"` - The workflow run is in progress
 * `"NEEDS_REVIEW"` - The workflow run requires manual review
 * `"REJECTED"` - The workflow run was rejected during manual review
 * `"PROCESSED"` - The workflow run completed successfully
 * `"FAILED"` - The workflow run encountered an error
    
</dd>
</dl>

<dl>
<dd>

**workflow_id:** `typing.Optional[str]` 

Filters workflow runs by the workflow ID. If not provided, runs for all workflows are returned. The ID will start with "workflow". This ID can be found when viewing a workflow on the Extend platform.

Example: `"workflow_BMdfq_yWM3sT-ZzvCnA3f"`
    
</dd>
</dl>

<dl>
<dd>

**file_name_contains:** `typing.Optional[str]` 

Filters workflow runs by the name of the file. Only returns workflow runs where the file name contains this string.

Example: `"invoice"`
    
</dd>
</dl>

<dl>
<dd>

**sort_by:** `typing.Optional[SortByEnum]` — Sorts the workflow runs by the given field.
    
</dd>
</dl>

<dl>
<dd>

**sort_dir:** `typing.Optional[SortDirEnum]` — Sorts the workflow runs in ascending or descending order. Ascending order means the earliest workflow run is returned first.
    
</dd>
</dl>

<dl>
<dd>

**next_page_token:** `typing.Optional[NextPageToken]` 
    
</dd>
</dl>

<dl>
<dd>

**max_page_size:** `typing.Optional[MaxPageSize]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.workflow_endpoints.<a href="src/fernstarterpack/workflow_endpoints/client.py">run_workflow</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Run a Workflow with files. A Workflow is a sequence of steps that process files and data in a specific order to achieve a desired outcome. A WorkflowRun will be created for each file processed. A WorkflowRun represents a single execution of a workflow against a file.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.workflow_endpoints.run_workflow(workflow_id='workflowId', )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**workflow_id:** `str` 

The ID of the workflow to run. The ID will start with "workflow". This ID can be found viewing the workflow on the Extend platform.

Example: `"workflow_BMdfq_yWM3sT-ZzvCnA3f"`
    
</dd>
</dl>

<dl>
<dd>

**files:** `typing.Optional[typing.Sequence[File4]]` — An array of files to process through the workflow. Either the `files` array or `rawTexts` array must be provided. Supported file types can be found [here](/developers/guides/supported-file-types).
    
</dd>
</dl>

<dl>
<dd>

**raw_texts:** `typing.Optional[typing.Sequence[str]]` — An array of raw strings. Can be used in place of files when passing raw data. The raw data will be converted to `.txt` files and run through the workflow. If the data follows a specific format, it is recommended to use the files parameter instead. Either `files` or `rawTexts` must be provided.
    
</dd>
</dl>

<dl>
<dd>

**version:** `typing.Optional[str]` 

An optional version of the workflow that files will be run through. This number can be found when viewing the workflow on the Extend platform. When a version number is not supplied, the most recent version of the workflow will be used. To run the `"draft"` version of a workflow, use `"draft"` as the version.

Examples:
- `"3"` - Run version 3 of the workflow
- `"draft"` - Run the draft version of the workflow
    
</dd>
</dl>

<dl>
<dd>

**priority:** `typing.Optional[int]` — An optional value used to determine the relative order of WorkflowRuns when rate limiting is in effect. Lower values will be prioritized before higher values.
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `typing.Optional[typing.Dict[str, typing.Optional[typing.Any]]]` — A optional metadata object that can be assigned to a specific WorkflowRun to help identify it. It will be returned in the response and webhooks. You can place any arbitrary `key : value` pairs in this object.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.workflow_endpoints.<a href="src/fernstarterpack/workflow_endpoints/client.py">get_workflow_run</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Once a workflow has been run, you can check the status and output of a specific WorkflowRun.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.workflow_endpoints.get_workflow_run(workflow_run_id='workflowRunId', )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**workflow_run_id:** `str` 

The ID of the WorkflowRun that was outputted after a Workflow was run through the API. The ID will start with "workflow_run". This ID can be found when creating a WorkflowRun via API, or when viewing the "history" tab of a workflow on the Extend platform.

Example: `"workflow_run_8k9m-xyzAB_Pqrst-Nvw4"`
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.workflow_endpoints.<a href="src/fernstarterpack/workflow_endpoints/client.py">update_workflow_run</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

You can update the name and metadata of an in progress WorkflowRun at any time using this endpoint.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.workflow_endpoints.update_workflow_run(workflow_run_id='workflowRunId', )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**workflow_run_id:** `str` 

The ID of the WorkflowRun. This ID will start with "workflow_run". This ID can be found in the API response when creating a Workflow Run, or in the "history" tab of a workflow on the Extend platform.

Example: `"workflow_run_8k9m-xyzAB_Pqrst-Nvw4"`
    
</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` — An optional name that can be assigned to a specific WorkflowRun
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `typing.Optional[typing.Dict[str, typing.Optional[typing.Any]]]` 

A metadata object that can be assigned to a specific WorkflowRun. If metadata already exists on this WorkflowRun, the newly incoming metadata will be merged with the existing metadata, with the incoming metadata taking field precedence.

You can include any arbitrary `key : value` pairs in this object.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.workflow_endpoints.<a href="src/fernstarterpack/workflow_endpoints/client.py">correct_workflow_run_outputs</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Use this endpoint to submit corrected outputs for a WorkflowRun for future processor evaluation and tuning in Extend.

If you are using our Human-in-the-loop workflow review, then we already will be collecting your operator submitted corrections. However, if you are receiving data via the API without human review, there could be incorrect outputs that you would like to correct for future usage in evaluation and tuning within the Extend platform. This endpoint allows you to submit corrected outputs for a WorkflowRun, by providing the correct output for a given output ID.

The output ID, would be found in a given entry within the outputs arrays of a [WorkflowRun](https://extendconfig.docs.buildwithfern.com/developers/objects/workflow-run) payload. The ID would look something like `dpr_gwkZZNRrPgkjcq0y-***`.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.workflow_endpoints.correct_workflow_run_outputs(workflow_run_id='workflowRunId', output_id='outputId', reviewed_output={'key': 'value'
}, )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**workflow_run_id:** `str` 

The ID of the workflow run that included this initial output. The ID will start with "workflow_run". This ID can be found when creating a WorkflowRun via API, or in the "history" tab of a workflow on the Extend platform.

Example: `"workflow_run_xKm9pNv3qWsY_jL2tR5Dh"`
    
</dd>
</dl>

<dl>
<dd>

**output_id:** `str` 

The ID of the output that these corrections are for. The ID will start with "dpr_".

Example: `"dpr_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**reviewed_output:** `typing.Dict[str, typing.Optional[typing.Any]]` 

The corrected output of the processor when run against the file.

This should be a JSON object conforming to the [output type schema](../../guides/output-types) of the given processor.

If this is an extraction result, you can include all fields, or just the ones that were corrected, our system will handle merges/dedupes. However, if you do include a field, we assume the value included in the final reviewed value.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.workflow_endpoints.<a href="src/fernstarterpack/workflow_endpoints/client.py">create_workflow</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new workflow in Extend. Workflows are sequences of steps that process files and data in a specific order to achieve a desired outcome.

This endpoint will create a new workflow in Extend, which can then be configured and deployed. Typically, workflows are created from our UI, however this endpoint can be used to create workflows programmatically. Configuration of the flow still needs to be done in the dashboard.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.workflow_endpoints.create_workflow(name='name', )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `str` — The name of the workflow
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## ProcessorEndpoints
<details><summary><code>client.processor_endpoints.<a href="src/fernstarterpack/processor_endpoints/client.py">run_processor</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Run processors (extraction, classification, splitting, etc.) on a given document
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.processor_endpoints.run_processor(processor_id='processorId', )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**processor_id:** `ProcessorId` 
    
</dd>
</dl>

<dl>
<dd>

**file:** `typing.Optional[File4]` 
    
</dd>
</dl>

<dl>
<dd>

**raw_text:** `typing.Optional[str]` — The raw text content of the file. This is included for all file types if the `rawText` query parameter is set to `true` in the endpoint request.
    
</dd>
</dl>

<dl>
<dd>

**version:** `typing.Optional[str]` 
    
</dd>
</dl>

<dl>
<dd>

**priority:** `typing.Optional[int]` 
    
</dd>
</dl>

<dl>
<dd>

**metadata:** `typing.Optional[typing.Dict[str, typing.Optional[typing.Any]]]` — An optional object that can be passed in to identify the run of the document processor. It will be returned back to you in the response and webhooks.
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[typing.Dict[str, typing.Optional[typing.Any]]]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.processor_endpoints.<a href="src/fernstarterpack/processor_endpoints/client.py">get_processor_run</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve details about a specific processor run, including its status, outputs, and any edits made during review
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.processor_endpoints.get_processor_run(id='id', )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` — The unique identifier of the processor run to retrieve
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.processor_endpoints.<a href="src/fernstarterpack/processor_endpoints/client.py">create_processor</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new processor in Extend, optionally cloning from an existing processor
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.processor_endpoints.create_processor(name='name', type="EXTRACT", )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `str` — The name of the new processor
    
</dd>
</dl>

<dl>
<dd>

**type:** `ProcessorType` 
    
</dd>
</dl>

<dl>
<dd>

**clone_processor_id:** `typing.Optional[str]` 

The ID of an existing processor to clone. The ID will start with "dp_".

Example: `"dp_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.processor_endpoints.<a href="src/fernstarterpack/processor_endpoints/client.py">get_processor_version</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a specific version of a processor in Extend
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.processor_endpoints.get_processor_version(processor_id='processorId', processor_version_id='processorVersionId', )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**processor_id:** `str` 

The ID of the processor. The ID will start with "dp_".

Example: `"dp_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**processor_version_id:** `str` 

The ID of the specific processor version to retrieve. The ID will start with "dpv_".

Example: `"dpv_QYk6jgHA_8CsO8rVWhyNC"`
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.processor_endpoints.<a href="src/fernstarterpack/processor_endpoints/client.py">list_processor_versions</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve all versions of a specific processor in Extend, including the current draft version
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.processor_endpoints.list_processor_versions(id='id', )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` 

The ID of the processor to retrieve versions for. The ID will start with "dp_".

Example: `"dp_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.processor_endpoints.<a href="src/fernstarterpack/processor_endpoints/client.py">publish_processor_version</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Publish a new version of an existing processor in Extend
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.processor_endpoints.publish_processor_version(id='id', release_type="major", )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` 

The ID of the processor to publish a new version for. The ID will start with "dp_".

Example: `"dp_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**release_type:** `PostProcessorsIdPublishRequestReleaseType` — The type of release for this version
    
</dd>
</dl>

<dl>
<dd>

**description:** `typing.Optional[str]` — A description of the changes in this version
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[typing.Dict[str, typing.Optional[typing.Any]]]` — Optionally supply a config object for this version of the processor
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.processor_endpoints.<a href="src/fernstarterpack/processor_endpoints/client.py">get_batch_processor_run</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve details about a batch processor run, including evaluation runs
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.processor_endpoints.get_batch_processor_run(id='id', )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` 

The unique identifier of the batch processor run to retrieve. The ID will start with "bpr_".

Example: `"bpr_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.processor_endpoints.<a href="src/fernstarterpack/processor_endpoints/client.py">update_processor</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update an existing processor in Extend
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.processor_endpoints.update_processor(id='id', )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` 

The ID of the processor to update. The ID will start with "dp_".

Example: `"dp_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**name:** `typing.Optional[str]` — The new name for the processor
    
</dd>
</dl>

<dl>
<dd>

**config:** `typing.Optional[typing.Dict[str, typing.Optional[typing.Any]]]` — The new configuration for the processor
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## FileEndpoints
<details><summary><code>client.file_endpoints.<a href="src/fernstarterpack/file_endpoints/client.py">list_files</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List files in your account. Files represent documents that have been uploaded to Extend.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.file_endpoints.list_files()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name_contains:** `typing.Optional[str]` — Filters files by the name of the file
    
</dd>
</dl>

<dl>
<dd>

**sort_dir:** `typing.Optional[GetFilesRequestSortDir]` — Sorts the files in ascending or descending order
    
</dd>
</dl>

<dl>
<dd>

**next_page_token:** `typing.Optional[str]` 

The token used to fetch the page of results from a previous request. We use cursor based pagination and will return a `nextPageToken` in the response if there are more results.

Note: If parameters other than `nextPageToken` change in subsequence requests, you are likely to receive incomplete results.

Example: `"xK9mLPqRtN3vS8wF5hB2cQ==:zWvUxYjM4nKpL7aDgE9HbTcR2mAyX3/Q+CNkfBSw1dZ="`
    
</dd>
</dl>

<dl>
<dd>

**max_page_size:** `typing.Optional[int]` — The maximum number of results to return in the response.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.file_endpoints.<a href="src/fernstarterpack/file_endpoints/client.py">create_file_deprecated</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new file in Extend for use in an evaluation set. This endpoint is deprecated, use /files/upload instead.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.file_endpoints.create_file_deprecated()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `typing.Optional[str]` — The name of the file
    
</dd>
</dl>

<dl>
<dd>

**url:** `typing.Optional[str]` — A pre signed URL for the file
    
</dd>
</dl>

<dl>
<dd>

**raw_text:** `typing.Optional[str]` — The raw text content of the file
    
</dd>
</dl>

<dl>
<dd>

**media_type:** `typing.Optional[str]` — The media type of the file (e.g. application/pdf)
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.file_endpoints.<a href="src/fernstarterpack/file_endpoints/client.py">get_file</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Fetch a file by its ID
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.file_endpoints.get_file(id='id', )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` 

Extend's ID for the file. It will always start with `"file_"`.

Example: `"file_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**raw_text:** `typing.Optional[bool]` — If set to true, the raw text content of the file will be included in the response. This is useful for indexing text-based files like PDFs, Word Documents, etc.
    
</dd>
</dl>

<dl>
<dd>

**markdown:** `typing.Optional[bool]` 

If set to true, the markdown content of the file will be included in the response. This is useful for indexing very clean content into RAG pipelines for files like PDFs, Word Documents, etc.

*Only available for files with a type of PDF, IMG.
*or .doc/.docx files that were auto-converted to PDFs.
    
</dd>
</dl>

<dl>
<dd>

**html:** `typing.Optional[bool]` 

If set to true, the html content of the file will be included in the response. This is useful for indexing html content into RAG pipelines for files like PDFs, Word Documents, etc.

*Only available for files with a type of DOCX.
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.file_endpoints.<a href="src/fernstarterpack/file_endpoints/client.py">create_evaluation_set</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new evaluation set in Extend
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.file_endpoints.create_evaluation_set(name='name', description='description', processor_id='processorId', )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `str` 

The name of the evaluation set.

Example: `"Invoice Processing Test Set"`
    
</dd>
</dl>

<dl>
<dd>

**description:** `str` 

A description of what this evaluation set is used for.

Example: `"Q4 2023 vendor invoices"`
    
</dd>
</dl>

<dl>
<dd>

**processor_id:** `str` 

The ID of the processor to create an evaluation set for. The ID will start with "dp_".

Example: `"dp_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.file_endpoints.<a href="src/fernstarterpack/file_endpoints/client.py">create_evaluation_set_item</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new evaluation set item
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.file_endpoints.create_evaluation_set_item(evaluation_set_id='evaluationSetId', file_id='fileId', expected_output={'key': 'value'
}, )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**evaluation_set_id:** `str` 

The ID of the evaluation set to add the item to. The ID will start with "ev_".

Example: `"ev_Xj8mK2pL9nR4vT7qY5wZ"`
    
</dd>
</dl>

<dl>
<dd>

**file_id:** `str` 

Extend's internal ID for the file. It will always start with "file_".

Example: `"file_xK9mLPqRtN3vS8wF5hB2cQ"`
    
</dd>
</dl>

<dl>
<dd>

**expected_output:** `typing.Dict[str, typing.Optional[typing.Any]]` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.file_endpoints.<a href="src/fernstarterpack/file_endpoints/client.py">update_evaluation_set_item</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update an evaluation set item by ID
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.file_endpoints.update_evaluation_set_item(id='id', expected_output={'key': 'value'
}, )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `str` 

The ID of the evaluation set item to update. The ID will start with "evi_".

Example: `"evi_kR9mNP12Qw4yTv8BdR3H"`
    
</dd>
</dl>

<dl>
<dd>

**expected_output:** `typing.Dict[str, typing.Optional[typing.Any]]` — The expected output of the processor when run against the file
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.file_endpoints.<a href="src/fernstarterpack/file_endpoints/client.py">bulk_create_evaluation_set_items</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create evaluation set items for a given evaluation set in bulk
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
from fernstarterpack.file_endpoints import PostEvaluationSetItemsBulkRequestItemsItem
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.file_endpoints.bulk_create_evaluation_set_items(evaluation_set_id='evaluationSetId', items=[PostEvaluationSetItemsBulkRequestItemsItem(file_id='fileId', expected_output={'key': 'value'
}, )], )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**evaluation_set_id:** `str` 

The ID of the evaluation set to add the items to. The ID will start with "ev_".

Example: `"ev_2LcgeY_mp2T5yPaEuq5Lw"`
    
</dd>
</dl>

<dl>
<dd>

**items:** `typing.Sequence[PostEvaluationSetItemsBulkRequestItemsItem]` — An array of objects representing the evaluation set items to create
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.file_endpoints.<a href="src/fernstarterpack/file_endpoints/client.py">upload_file</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Upload and create a new file in Extend
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.file_endpoints.upload_file()

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**file:** `from __future__ import annotations
core.File` — See core.File for more documentation
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## ParseEndpoints
<details><summary><code>client.parse_endpoints.<a href="src/fernstarterpack/parse_endpoints/client.py">parse_file</a>(...)</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Parse files to get cleaned, chunked target content (e.g. markdown)
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```python
from fernstarterpack import Starter
from fernstarterpack.parse_endpoints import PostParseRequestFile
from fernstarterpack.parse_endpoints import PostParseRequestConfig
client = Starter(extend_api_version="YOUR_EXTEND_API_VERSION", token="YOUR_TOKEN", )
client.parse_endpoints.parse_file(file=PostParseRequestFile(), config=PostParseRequestConfig(), )

```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**file:** `PostParseRequestFile` 
    
</dd>
</dl>

<dl>
<dd>

**config:** `PostParseRequestConfig` 
    
</dd>
</dl>

<dl>
<dd>

**request_options:** `typing.Optional[RequestOptions]` — Request-specific configuration.
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

