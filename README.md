NAME
    imapsync - IMAP synchronisation, sync, copy or migration tool.
    Synchronises mailboxes between two imap servers. Good at IMAP migration.
    More than 52 different IMAP server softwares supported with success, few
    failures.

    $Revision: 1.644 $

SYNOPSIS
    To synchronize imap account "foo" on "imap.truc.org" to imap account
    "bar" on "imap.trac.org" with foo password "secret1" and bar password
    "secret2":

      imapsync \
       --host1 imap.truc.org --user1 foo --password1 secret1 \
       --host2 imap.trac.org --user2 bar --password2 secret2

INSTALL
     imapsync works fine under any Unix OS with perl.
     imapsync works fine under Windows (2000, XP, Vista, Seven) 
     with Strawberry Perl (5.10, 5.12 or higher)
     or as a standalone binary software imapsync.exe

    imapsync can be available directly on the following distributions:
    FreeBSD, Debian, Ubuntu, Gentoo, Fedora, NetBSD, Darwin, Mandriva and
    OpenBSD. See http://oswatershed.org/pkg/imapsync

     Purchase latest imapsync at
     http://imapsync.lamiral.info/

     You'll receive a link to a compressed tarball called imapsync-x.xx.tgz
     where x.xx is the version number. Untar the tarball where
     you want (on Unix):

     tar xzvf  imapsync-x.xx.tgz

     Go into the directory imapsync-x.xx and read the INSTALL file.
     The INSTALL file can be found at 
     http://imapsync.lamiral.info/INSTALL
     It is now split in several files for each system
     http://imapsync.lamiral.info/INSTALL.d/

     The frozen freecode (was freshmeat) record is at 
     http://freecode.com/projects/imapsync

USAGE
     imapsync [options]

    To get a description of each option just run imapsync like this:

      imapsync --help

    or simply

      imapsync

    This description of all options is available at
    http://imapsync.lamiral.info/OPTIONS

    The option list:

      imapsync [--host1 server1]  [--port1 <num>]
               [--user1 <string>] [--passfile1 <string>]
               [--host2 server2]  [--port2 <num>]
               [--user2 <string>] [--passfile2 <string>]
               [--ssl1] [--ssl2]
               [--tls1] [--tls2]
               [--authmech1 <string>] [--authmech2 <string>]
               [--proxyauth1] [--proxyauth2]
               [--domain1] [--domain2] 
               [--authmd51] [--authmd52]
               [--folder <string> --folder <string> ...]
               [--folderrec <string> --folderrec <string> ...]
               [--include <regex>] [--exclude <regex>]
               [--prefix2 <string>] [--prefix1 <string>] 
               [--regextrans2 <regex> --regextrans2 <regex> ...]
               [--sep1 <char>]
               [--sep2 <char>]
               [--justfolders] [--justfoldersizes] [--justconnect] [--justbanner]
               [--syncinternaldates]
               [--idatefromheader]
               [--syncacls]
               [--regexmess <regex>] [--regexmess <regex>]
               [--skipmess <regex>] [--skipmess <regex>]
               [--maxsize <int>]
               [--minsize <int>]
               [--maxage <int>]
               [--minage <int>]
               [--search <string>]
               [--search1 <string>]
               [--search2 <string>]
               [--useheader <string>] [--useheader <string>]
               [--nouid1] [--nouid2] 
               [--usecache]
               [--noskipsize]
               [--delete] 
               [--delete2] [--delete2duplicates] 
               [--expunge] [--expunge1] [--expunge2] [--uidexpunge2]
               [--delete2folders] [--delete2foldersonly] [--delete2foldersbutnot]
               [--subscribed] [--subscribe] [--subscribeall] 
               [--nofoldersizes] [--nofoldersizesatend] 
               [--dry]
               [--debug] [--debugimap][--debugimap1][--debugimap2] [--debugcontent]
               [--timeout <int>]  
               [--noreleasecheck]
               [--releasecheck]
               [--pidfile <filepath>] [--pidfilelocking]
               [--tmpdir  <dirpath>]
               [--nolog] 
               [--logfile <filepath>]
               [--version] [--help]
               [--tests] [--testsdebug] [--testslive]

DESCRIPTION
    Imapsync command is a tool allowing incremental and recursive imap
    transfers from one mailbox to another.

    By default all folders are transferred, recursively, all possible flags
    (\Seen \Answered \Flagged etc.) are synced too.

    We sometimes need to transfer mailboxes from one imap server to another.
    This is called migration.

    Imapsync reduces the amount of data transferred by not transferring a
    given message if it resides already on both sides. Same specific headers
    and the transfer is done only once; taken into account are by default
    Message-Id and Received header lines. All flags are preserved, unread
    will stay unread, read will stay read, deleted will stay deleted. You
    can stop the transfer at any time and restart it later, imapsync works
    well with bad connections and interruptions.

    You can decide to delete the messages from the source mailbox after a
    successful transfer, it can be a good feature when migrating live
    mailboxes since messages will be only on one side. In that case, use the
    --delete option. Option --delete implies also option --expunge so all
    messages marked deleted on host1 will be really deleted. (you can use
    --noexpunge to avoid this but I don't see any good real world scenario
    for the combination --delete --noexpunge).

    A different scenario is synchronizing a mailbox B from another mailbox A
    in case you just want to keep a "live" copy of A in B. In that case
    --delete2 has to be used, it deletes messages in host2 folder B that are
    not in host1 folder A. If you also need to destroy host2 folders that
    are not in host1 then use --delete2folders (see also
    --delete2foldersonly and --delete2foldersbutnot).

    Imapsync is not adequate for maintaining two active imap accounts in
    synchronization when the user plays independently on both sides. Use
    offlineimap (written by John Goerzen) or mbsync (written by Michael R.
    Elkins) for 2 ways synchronizations.

OPTIONS
    To get a description of each option just invoke:

      imapsync

    or read http://imapsync.lamiral.info/OPTIONS

HISTORY
    I wrote imapsync because an enterprise (basystemes) paid me to install a
    new imap server without losing huge old mailboxes located on a far away
    remote imap server accessible by a low bandwidth link. The tool imapcp
    (written in python) could not help me because I had to verify every
    mailbox was well transferred and delete it after a good transfer.
    imapsync started its life as a copy_folder.pl patch. The tool
    copy_folder.pl comes from the Mail-IMAPClient-2.1.3 perl module tarball
    source (in the examples/ directory of the tarball).

EXAMPLE
    While working on imapsync parameters please run imapsync in dry mode (no
    modification induced) with the --dry option. Nothing bad can be done
    this way.

    To synchronize the imap account "buddy" (with password "secret1") on
    host "imap.src.fr" to the imap account "max" (with password "secret2")
    on host "imap.dest.fr":

     imapsync --host1 imap.src.fr  --user1 buddy --password1 secret1 \
              --host2 imap.dest.fr --user2 max   --password2 secret2

    Then you will have max's mailbox updated from buddy's mailbox.

SECURITY
    You can use --passfile1 instead of --password1 to give the password
    since it is safer. With --password1 option any user on your host can see
    the password by using the 'ps auxwwww' command. Using a variable (like
    $PASSWORD1) is also dangerous because of the 'ps auxwwwwe' command. So,
    saving the password in a well protected file (600 or rw-------) is the
    best solution.

    imasync is not totally protected against sniffers on the network since
    passwords may be transferred in plain text if CRAM-MD5 is not supported
    by your imap servers. Use --ssl1 (or --tls1) and --ssl2 (or --tls2) to
    enable encryption on host1 and host2.

    You may authenticate as one user (typically an admin user), but be
    authorized as someone else, which means you don't need to know every
    user's personal password. Specify --authuser1 "adminuser" to enable this
    on host1. In this case, --authmech1 PLAIN will be used by default since
    it is the only way to go for now. So don't use --authmech1 SOMETHING
    with --authuser1 "adminuser", it will not work. Same behavior with the
    --authuser2 option. Authenticate with an admin account must be supported
    by your imap server to work with imapsync.

    When working on Sun/iPlanet/Netscape IMAP servers you must use
    --proxyauth1 to enable administrative user to masquerade as another
    user. Can also be used on destination server with --proxyauth2

    You can authenticate with OAUTH when transfering from Google Apps. The
    consumer key will be the domain part of the --user, and the --password
    will be used as the consumer secret. It does not work with Google Apps
    free edition.

EXIT STATUS
    imapsync will exit with a 0 status (return code) if everything went
    good. Otherwise, it exits with a non-zero status.

    So if you have an unreliable internet connection, you can use this loop
    in a Bourne shell:

            while ! imapsync ...; do 
                  echo imapsync not complete
            done

LICENSE
    imapsync is free, open, public but not always gratis software cover by
    the NOLIMIT Public License. See the LICENSE file included in the
    distribution or just read this simple sentence as it is the licence
    text: No limit to do anything with this work and this license.

MAILING-LIST
    The public mailing-list may be the best way to get free support.

    To write on the mailing-list, the address is:
    <imapsync@linux-france.org>

    To subscribe, send any message (even empty) to:
    <imapsync-subscribe@listes.linux-france.org> then just reply to the
    confirmation message.

    To unsubscribe, send a message to:
    <imapsync-unsubscribe@listes.linux-france.org>

    To contact the person in charge for the list:
    <imapsync-request@listes.linux-france.org>

    The list archives are available at:
    http://www.linux-france.org/prj/imapsync_list/ So consider that the list
    is public, anyone can see your post. Use a pseudonym or do not post to
    this list if you want to stay private.

    Thank you for your participation.

AUTHOR
    Gilles LAMIRAL <gilles.lamiral@laposte.net>

    Feedback good or bad is very often welcome.

    Gilles LAMIRAL earns his living by writing, installing, configuring and
    teaching free, open and often gratis softwares. It used to be "always
    gratis" but now it is "often" because imapsync is sold by its author, a
    good way to stay maintening and supporting free open public softwares
    (see the license) over decades.

BUG REPORT GUIDELINES
    Help me to help you: follow the following guidelines.

    Report any bugs or feature requests to the public mailing-list or to the
    author.

    Before reporting bugs, read the FAQ, the README and the TODO files.
    http://imapsync.lamiral.info/

    Upgrade to last imapsync release, maybe the bug is already fixed.

    Upgrade to last Mail-IMAPClient Perl module.
    http://search.cpan.org/dist/Mail-IMAPClient/ maybe the bug is already
    fixed there.

    Make a good title with word "imapsync" in it (my spam filters won't
    filter it), Try to write an email title with more words than just
    "imapsync" or "problem", a good title is made of keywords summary, but
    not too long (one visible line).

    Help us to help you: in your report, please include:

     - imapsync version.

     - output near the first failures, a few lines before is good to get the context
       of the issue. First failures messages are often more significant than 
       the last ones. 
 
     - if the issue is always related to the same messages, include the output 
       with --debug --debugimap, near the failure point. For example,
       Isolate a buggy message or two in a folder 'BUG' and use 

         imapsync ... --folder 'BUG' --debug --debugimap 

     - imap server softwares on both sides and their version number.

     - imapsync with all the options you use,  the full command line
       you use (except the passwords of course). 

     - IMAPClient.pm version.

     - the run context. Do you run imapsync.exe, a unix binary 
       or the perl script imapsync.

     - operating system running imapsync.

     - virtual software context (vmware, xen etc.)

     - operating systems on both sides and the third side in case
       you run imapsync on a foreign host from the both.

    Most of those values can be found as a copy/paste at the begining of the
    output, so a carbon copy of the output is a very easy and very good
    debug report for me.

    One time in your life, read the paper "How To Ask Questions The Smart
    Way" http://www.catb.org/~esr/faqs/smart-questions.html and then forget
    it.

IMAP SERVERS
    See http://imapsync.lamiral.info/S/imapservers.shtml

HUGE MIGRATION
    Pay special attention to options --subscribed --subscribe --delete
    --delete2 --delete2folders --maxage --minage --maxsize --useuid
    --usecache

    If you have many mailboxes to migrate think about a little shell
    program. Write a file called file.txt (for example) containing users and
    passwords. The separator used in this example is ';'

    The file.txt file contains:

    user001_1;password001_1;user001_2;password001_2
    user002_1;password002_1;user002_2;password002_2
    user003_1;password003_1;user003_2;password003_2
    user004_1;password004_1;user004_2;password004_2
    user005_1;password005_1;user005_2;password005_2 ...

    On Unix the shell program can be:

     { while IFS=';' read  u1 p1 u2 p2; do 
            imapsync --host1 imap.side1.org --user1 "$u1" --password1 "$p1" \
                     --host2 imap.side2.org --user2 "$u2" --password2 "$p2" ...
     done ; } < file.txt

    On Windows the batch program can be:

      FOR /F "tokens=1,2,3,4 delims=; eol=#" %%G IN (file.txt) DO imapsync ^
      --host1 imap.side1.org --user1 %%G --password1 %%H ^
      --host2 imap.side2.org --user2 %%I --password2 %%J ...

    The ... have to be replaced by nothing or any imapsync option. Welcome
    in shell programming !

    You will find already written scripts at
    http://imapsync.lamiral.info/examples/

Hacking
    Feel free to hack imapsync as the NOLIMIT license permits it.

Links
    Entries for imapsync:
    https://web.archive.org/web/20070202005121/http://www.imap.org/products/
    showall.php

SIMILAR SOFTWARES
      imap_tools    : http://www.athensfbc.com/imap_tools
      offlineimap   : https://github.com/nicolas33/offlineimap
      mbsync        : http://isync.sourceforge.net/
      mailsync      : http://mailsync.sourceforge.net/
      mailutil      : http://www.washington.edu/imap/
                      part of the UW IMAP tookit.
      imaprepl      : http://www.bl0rg.net/software/
                      http://freecode.com/projects/imap-repl/
      imapcopy      : http://home.arcor.de/armin.diehl/imapcopy/imapcopy.html
      migrationtool : http://sourceforge.net/projects/migrationtool/
      imapmigrate   : http://sourceforge.net/projects/cyrus-utils/
      wonko_imapsync: http://wonko.com/article/554
                      see also file W/tools/wonko_ruby_imapsync
      exchange-away : http://exchange-away.sourceforge.net/
      pop2imap      : http://www.linux-france.org/prj/pop2imap/

    Feedback (good or bad) will often be welcome.

    $Id: imapsync,v 1.644 2015/07/17 01:22:52 gilles Exp gilles $
