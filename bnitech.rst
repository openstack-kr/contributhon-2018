[��Ʈ������ 2018] ���½��� 2��: ���� ���� ���� (8/31 ��, ���� 7��) ����
+++++++++++++++++++++++++++++++++++++++++++++
ī��24 ���� Ȯ��
	* ���� �����Ȳ
		* 1.234.**.***
		* ���� �ӽ����� Ȯ��
			* ����
				* root
			* IPMI ����
				* b******
			* �ӽ� ��й�ȣ
				* a*******

    Varant�� ��ġ
	* �������� �νð� �缳ġ �Ҽ� �ִ� ȯ��

		* ����ȯ���� ���� ���½����� ��ġ�Ѵ�.
		* �׷� ������ �ٽ� �����ϱ� ��������.
	* ����ȯ���� �ڵ�� ������ �� �ְ� ���ش�.
	* VM�� ������ ���� �׽�Ʈ���� ���� ������.

���½��� ��ġ
	* yum install -y binutils gcc make patch libgomp dkms glibc-headers glibc-devel kernel-headers kernel-devel

		* �ʿ��� ��Ű�� ��ġ
	* wget https://download.virtualbox.org/virtualbox/5.2.18/VirtualBox-5.2-5.2.18_124319_el6-1.x86_64.rpm
	* rpm �ȵǼ���ġ

		* �ƴҼ���

			* wget https://rpmfind.net/linux/centos/6.10/os/x86_64/Packages/SDL-1.2.14-7.el6_7.1.i686.rpm
			* wget https://rpmfind.net/linux/centos/6.10/os/x86_64/Packages/mesa-libGL-11.0.7-4.el6.i686.rpm
			* wget https://rpmfind.net/linux/centos/6.10/os/x86_64/Packages/libXmu-1.1.1-2.el6.x86_64.rpm
		* wget -O /etc/yum.repos.d/virtualbox.repo http://download.virtualbox.org/virtualbox/rpm/rhel/virtualbox.repo
		* yum list VirtualBox*
		* yum update
		* yum install VirtualBox-5.2
	* rpm -ivh https://releases.hashicorp.com/vagrant/2.1.4/vagrant_2.1.4_x86_64.rpm


	* ��Ű��ó

		* PENCIL�� �׸�

			* ����1
	* root�� contributon ���� �����

		* �ȿ���
		* vagrantfile����

			* Vagrant.configure("2") do |config|
			*   config.vm.box = "ubuntu/xenial64"
			* end
		* �ۼ�
	* vagrant up
	* vagrant status

		* ����Ȯ��
	* vagrant ssh

		* vatrantfile�� �ִ°�����
		* ����ӽ� ����
	* vagrant destroy

		* ����ӽ� ����
	* vagrant up ���� ����� ����

		* ó������ ������ �ȴ�.
		* ���ÿ� �⺻ ���ϵ��� �ٿ�Ǿ��־
	* ubuntu (���󼭹�) ���� �۾�

		* logout

			* ������
	* vagrant ����

		* config.vm.provider "virtualbox" do |vb|
		*       vb.memory = "6144"
		*       vb.cpus = "6"
		*   end
	* �ڵ�� ������ ������ �� �ִ�.
	* �������� ��α׿���

		* https://nhnent.dooray.com/share/posts/NksDQdLvSA-KRSuJra5jlA
		* virtualbox ��Ʈ��ũ ����

			* host-only networking �̿�
		* vagrant networking ��

			* Forwarded port

				* https://www.vagrantup.com/docs/networking/forwarded_ports.html
		* vagrantfile ����

			*  config.vm.network "forwarded_port", guest: 80, host: 8080
			* �߰�
		* vagrant reload
		* NAT IP�� ���ӺҰ� ��
	* snapshot ����
	* ���κ����׵� ����
	* ��Ŀ�� �����̳�

		* vagrant�� VM
	* vm �̸��� ���� ����
	* ���� vagrantfile

		* Vagrant.configure("2") do |config|
		*   config.vm.box = "ubuntu/xenial64"
		*   config.vm.provider "virtualbox" do |vb|
		*       vb.memory = "6144"
		*       vb.cpus = "6"
		*   end
		* config.vm.network "forwarded_port", guest: 80, host: 8080
		* end
	* devstack ��ġ

		* https://docs.openstack.org/devstack/latest/

			* download devstack ���� ����
		* git branch -l

			* �귣ġȮ��
			* git branch -r
		* master �귣ġ���� �ϸ� Ȯ��
		* git checkout stable/pike
		* git status

			* �귣ġȮ��
		* local.conf ���� �����

			* [[local|localrc]]
			* HOST_IP=10.0.2.15

				* �⺻ ����
			* ADMIN_PASSWORD=secret
			* DATABASE_PASSWORD=$ADMIN_PASSWORD
			* RABBIT_PASSWORD=$ADMIN_PASSWORD
			* SERVICE_PASSWORD=$ADMIN_PASSWORD
		* ./stack.sh

			* �����ɸ�
			* �⺻���� ��� ���� ��ġ
		* ���ξ����Ƿ� ����

			* admin
			* secret
	* screen

		* ������ ȭ���� ����
		* yum install screen
		* screen -S devstack
		* ctrl+a,d
		* screen -list
		* screen -r �̸�
		* screen session ����� ����� �Ʒ��� �����ϴ�.

			* screen -X -S [���ְ� ���� ���� ����] quit
		* ��׶���� ���డ������
		* �۾��ϴ� ȯ�� ����������

����� �
	* rst �������� ���

		* https://www.slideshare.net/ianychoi/pycon-kr-2017-rst-python-openstack

			* RST ���� �ۼ� ����

		* ���߻Ӹ��ƴ϶� ����ȭ�� �߿��ϴ�

			* http://git.openstack.org/cgit
			* https://docs.openstack.org/ko_KR/upstream-training/
	* spec

		* �����ϰ������ ����δ� ��
	* ����ҿ� ���� �ۼ��ϴ¹�

		* ����Ҹ� fork�Ѵ�.
		* ��������
		* �����Ǿ�
		* ��������� �����.
		* $ ssh-keygen -t rsa -b 4096

			* ������ Ű ����꿡 �Է�
		* tect.ssut

			* git �ۼ� ����


