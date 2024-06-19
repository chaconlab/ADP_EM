# ADP_EM

A multiresolution rigid-body fitting tool that uses spherical harmonics to effectively speed up the rotational part of the fitting search
This tool makes it possible to accurately dock atomic structures into low-resolution electron-density maps in times ranging from seconds to a few minutes. 

-J.I. Garzón, J.A. Kovacs, R. Abagyan, and P. Chacón. (2007) ADP_EM: Fast exhaustive multi-resolution docking for high-throughput coverage. Bioinformatics. 23(4):427-33<a href="http://www.ncbi.nlm.nih.gov/pubmed/17150992"><img src="https://chaconlab.org/images/publications/pubmed.jpg" alt="abs" border="0" /></a> <a href="https://chaconlab.org/PDF/2007_adp_em.pdf"><img src="https://chaconlab.org/images/publications/acrobaticon4.gif" alt="pdf" border="0" /></a></p>

Here we give a brief overview of the necessary steps to run the program, but we strongly encourage you to follow the tutorials. The user guide is partitioned into three levels of usage: i) Basic single fitting, ii) multiple fitting iii) Advanced options


## Single fitting

For fitting a single atomic structure, a collection of atomic structures or an EM density map into an EM density map enter the following command at the prompt:
<div class="box-content">adp_em &lt;em map&gt; &lt;pdb/map/list&gt; &lt;bw&gt; &lt;cutoff&gt; &lt;resolution/cutoff&gt;</div>
<p>where:</p>
<table style="width: 620px; height: 485px;" border="2"><colgroup> <col width="70" /> <col width="472" /> </colgroup>
<tbody>
<tr>
<td bgcolor="#f0f0f0" width="70">
<p>em map</p>
</td>
<td width="472">
<p>Filename of the fitting 3D frame.</p>
<p>3D electron microscopy experimental map. Situs and CCP4 formats are only accepted with extensions ".sit" and ".cpp4". Be careful with the byte-order/architecture.</p>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="70">
<p>pdb/map/list</p>
</td>
<td width="472">
<p>Filename be fitted. Depending on the extension:</p>
<ul style="list-style-type: circle;">
<li>To fit a single atomic structure a file with extension ".pdb" or ".mol" is expected.</li>
<li>To fit a 3D electron map use files with extension ".ccp4" or ".sit".</li>
<li>If multiple option is set (-m) then a text file with a list of PDB filenames is expected</li>
</ul>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="70">
<p>bw</p>
</td>
<td width="472">
<p>Bandwidth used in the harmonic transformation. It must be an even number. The default value is 16. Higher values can be used (e.g. 24 or 32) for docking cases where additional rotational accuracy is needed or for large structures. Remember that the computational cost increases with this parameter.</p>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="70">
<p>Cutoff</p>
</td>
<td width="472">
<p>Density threshold value for the experimental map. All density levels below this value will be discarted.</p>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="70">
<p>resolution/cutoff</p>
</td>
<td width="472">
<p>Depending on the type of element to fit:</p>
<ul style="list-style-type: circle;">
<li>If a Pdb file/s are fitted: Nominal resolution of the projection map in Å. Our resolution criterion follows EMAN critera (e.g. PDB2MRC tool)</li>
<li>If a 3d map is fitted: Density threshold value for the fitted map</li>
</ul>
</td>
</tr>
</tbody>
</table>
<p> </p>

## Multiple fitting

For fitting multiple atomic structures into an EM density map use:
<div class="box-content">&gt;adp_em &lt;EM map&gt; &lt;pdb&gt; &lt;bw&gt; &lt;cutoff&gt; &lt;resolution&gt; -m</div>
<p>Exactly the same parameters as before with the exception of:</p>
<table style="width: 550px;" border="2"><colgroup> <col width="54" /> <col width="488" /> </colgroup>
<tbody>
<tr>
<td bgcolor="#f0f0f0" width="54">
<p>-m</p>
</td>
<td width="488">
<p>This option tells the program that multiple atomic structures will be provided</p>
</td>
</tr>
</tbody>
</table>

## Advanced options

Many optional parameters can be used for tuning up the docking tool. The more useful are:</p>
<table style="width: 550px;" border="2"><colgroup> <col width="54" /> <col width="488" /> </colgroup>
<tbody>
<tr>
<td bgcolor="#f0f0f0" width="54">
<p>−h</p>
</td>
<td width="488">
<p>Displays usage information and exits</p>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="54">
<p>−f &lt;int&gt;</p>
</td>
<td width="488">
<p>This option sets the fitting criterion used:</p>
<ul>
<li>
<p><i>0 </i>Standard linear cross-correlation. The scalar product between the density maps of the low resolution map and the low-pass filtered atomic structure. Recommended for resolutions &lt; 15Å and when the atomic model accounts for all the density of the map.</p>
</li>
<li>
<p><i>1 </i>[default] A Laplacian filter is applied by default to maximize the fitting contrast. Recommended for resolutions &gt; 15Å and when the atomic model only accounts for a part of the density of the experimental map.</p>
</li>
</ul>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="54">
<p>−n &lt;int&gt;</p>
</td>
<td width="488">
<p>Number of saved solutions (default 50)</p>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="54">
<p>−t &lt;float&gt;</p>
</td>
<td width="488">
<p>Translational sampling in Å (default twice of voxel size). Values &gt;6Å should be not used.</p>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="54">
<p>−s &lt;int&gt;</p>
</td>
<td width="488">
<p>Translational scan strategy:</p>
<ul>
<li>
<p><i>0 </i>Full search. All the translational points inside the target EM map will be explored.</p>
</li>
<li>
<p><i>1 </i>Limited. Radial search starting from the center of mass</p>
</li>
<li>
<p><i>2 </i>[default] Masking search.</p>
</li>
</ul>
</td>
</tr>
</tbody>
</table>
<p><br />Other options for expert users:</p>
<table style="width: 550px; height: 422px;" border="2"><colgroup> <col width="123" /> <col width="419" /> </colgroup>
<tbody>
<tr>
<td bgcolor="#f0f0f0" width="123">
<p>−−ne &lt;int&gt;</p>
</td>
<td width="419">
<p>Number peaks explored per docking (-m) (default 30)</p>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="123">
<p>−−np &lt;int&gt;</p>
</td>
<td width="419">
<p>Number peaks stored per iteration (default 20)</p>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="123">
<p>−−nr &lt;int&gt;</p>
</td>
<td width="419">
<p>Number peaks stored in the search (default 100)</p>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="123">
<p>−−nrm &lt;int&gt;</p>
</td>
<td width="419">
<p>Number peaks stored in the multi-docking search (default 500)</p>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="123">
<p>−−rt &lt;float&gt;</p>
</td>
<td width="419">
<p>Translational threshold in grid units (default 2.0)</p>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="123">
<p>−−rc &lt;float&gt;</p>
</td>
<td width="419">
<p>Rotational threshold in degrees (default 360/bw)</p>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="123">
<p>−−lw &lt;float&gt;</p>
</td>
<td width="419">
<p>Width between spherical layers (default 1.0)</p>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="123">
<p>−−cutoff2 &lt;float&gt;</p>
</td>
<td width="419">
<p>Density cutoff of the simulated map (default 0.0)</p>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="123">
<p>-R</p>
</td>
<td width="419">
<p>Reference PDB to compute rmsd</p>
</td>
</tr>
<tr>
<td bgcolor="#f0f0f0" width="123">
<p>-i</p>
</td>
<td width="419">
<p>Turn off interpolation local improvement of solutions</p>
</td>
</tr>
</tbody>
</table>



