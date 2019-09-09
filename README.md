<!--  [View this file Online]  https://github.com/mcavallo-git/cloud-infrastructure/blob/master/README.md  -->

<h3>Cloud Infrastructure</h3>
<hr />
<ul>

<!-- ------------------------------------------------------------ -->

<li><details><summary>
		<strong>Setup Repository Sync</strong>
		<sub> → <i>Syncs git repository & all runtime shellscripts</i></sub>
	</summary>
	<br />
	<ol>
		<li>Download and run the cloud-sync shellscript from the git-repo by calling:<br /><pre><code>REPO_FILE="https://raw.githubusercontent.com/mcavallo-git/cloud-infrastructure/master/usr/local/sbin/sync_cloud_infrastructure" && LOCAL_FILE="${HOME}/sync_cloud_infrastructure" && wget "${REPO_FILE}" --output-document="${LOCAL_FILE}" && chmod 0700 "${LOCAL_FILE}" && ${LOCAL_FILE} --cron sync && rm "${LOCAL_FILE}";</code></pre></li>
	</ol>
<hr /></details></li>

<!-- ------------------------------------------------------------ -->

<li><details><summary>
		<strong>Setup Packages</strong>
		<sub> → <i>Setup/Configure Required Linux Packages</i></sub>
	</summary>
	<br />
	<ol>
		<li>Install utility/devops-tool packages by calling: <pre><code>sudo install_apt_packages;</code></pre><sub> ⚠️ This step assumes that <code>/usr/local/bin</code> & <code>/usr/local/sbin</code> have been synced (populated) from the git repository via command <code>sync_cloud_infrastructure</code></sub></li>
	</ol>
<hr /></details></li>

<!-- ------------------------------------------------------------ -->

<li><details><summary>
		<strong>Setup User-Level Security</strong>
		<sub> → <i>Create/Configure Required Linux SSH Policies (no Multifactor Authentication)</i></sub>
	</summary>
	<br />
	<ol>
		<li>Create a backup snapshot of EBS Volume via the AWS Dashboard @ https://console.aws.amazon.com/ec2#Snapshots</li><br />
		<li>Run the following line of code to modify the ssh configuration script by [ backing-up the existing script ] & [ updating the script to require public-key authentication ]: <pre><code>SSHD_CONFIG="/etc/ssh/sshd_config"; cp -f "${SSHD_CONFIG}" "${SSHD_CONFIG}.$(date +'%Y%m%d_%H%M%S')"; REPO_FILE="https://raw.githubusercontent.com/mcavallo-git/cloud-infrastructure/master/etc/ssh/sshd_config.no_mfa" && LOCAL_FILE="${SSHD_CONFIG}.no_mfa" && wget "${REPO_FILE}" --output-document="${LOCAL_FILE}" && chmod 0644 "${LOCAL_FILE}" && cp -f "${LOCAL_FILE}" "${SSHD_CONFIG}"; service ssh restart;</code></pre></li>
	</ol>
<hr /></details></li>

<!-- ------------------------------------------------------------ -->

<li><details><summary>
		<strong>Setup User-Level Security (+MFA)</strong>
		<sub> → <i>Create/Configure Required Linux SSH Policies to incorporate Duo MFA (Multifactor Authentication)</i></sub>
	</summary>
	<br />
	<ol>
		<li>Follow Duo's updated installation guide for their pam_duo module, which may be found @ <b>https://duo.com/docs/duounix</b> → refer to section titled: <b>Install pam_duo</b></li><br />
		<li>Once previous step is complete, run the following line of code to modify the ssh configuration script by [ backing-up the existing script ] & [ updating the script to require public-key AND multifactor authentication ]: <pre><code>SSHD_CONFIG="/etc/ssh/sshd_config"; cp -f "${SSHD_CONFIG}" "${SSHD_CONFIG}.$(date +'%Y%m%d_%H%M%S')"; REPO_FILE="https://raw.githubusercontent.com/mcavallo-git/cloud-infrastructure/master/etc/ssh/sshd_config.mfa" && LOCAL_FILE="${SSHD_CONFIG}.mfa" && wget "${REPO_FILE}" --output-document="${LOCAL_FILE}" && chmod 0644 "${LOCAL_FILE}" && cp -f "${LOCAL_FILE}" "${SSHD_CONFIG}"; service ssh restart;</code></pre></li>
	</ol>
<hr /></details></li>

<!-- ------------------------------------------------------------ -->


<li><details><summary>
		<strong>Citation(s)</strong>
	</summary>
	<ul>
		<li><h4><a href="usr/local/share/man/hier.man"><pre><code>man hier;   # hier - description of the filesystem hierarchy</pre></code></a></h4></li><br />
		<li><h4><a href="https://linux.die.net/man/7/hier"><pre><code>hier(7) - Linux man page</pre></code></a></h4></li><br />
		<li><h4><a href="https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard"><pre><code>Filesystem Hierarchy Standard (FHS)</pre></code></a></h4></li><br />
	</ul>
<hr /></details></li>

<!-- ------------------------------------------------------------ -->

</ul>